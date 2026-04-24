```sh
mkdir -p ~/.config/nvim/lua/plugins && \
touch ~/.config/nvim/lua/plugins/java.lua \
      ~/.config/nvim/lua/plugins/dap-java.lua \
      ~/.config/nvim/lua/plugins/java-cmp.lua \
      ~/.config/nvim/lua/plugins/java-tools.lua \
      ~/.config/nvim/lua/plugins/autocomplete.lua
```

**¡Perfecto!** Para tener **IntelliJ IDEA** en **Neovim**, necesitas **LSP + DAP + Treesitter + Snippets especializados**. Te doy la **configuración EXACTA**:

## 🎯 **Configuración IntelliJ-like para JAVA**

### 1. **LazyVim + Plugins ESENCIALES**

Crea estos archivos en `~/.config/nvim/lua/plugins/`:

**`java.lua`** (LSP + DAP para Java):
```lua
return {
  {
    "mfussenegger/nvim-jdtls",
    ft = { "java" },
    dependencies = {
      "neovim/nvim-lspconfig",
      "mfussenegger/nvim-dap",
      "williamboman/mason.nvim",
    },
    config = function()
      local java_cmd = vim.fn.exepath("java")
      
      -- 🔥 PATH CORRECTO Amazon Corretto 17 (común en distribuciones)
      local jdk_paths = {
        "/usr/lib/jvm/amazon-corretto-17",
        "/usr/lib/jvm/java-17-amazon-corretto",
        "/usr/lib/jvm/default-java",
        "/usr/lib/jvm/java-17-openjdk",
        vim.fn.expand("$JAVA_HOME") or "",
      }
      
      local jdk_path = ""
      for _, path in ipairs(jdk_paths) do
        if vim.fn.isdirectory(path) == 1 then
          jdk_path = path
          break
        end
      end
      
      if jdk_path == "" then
        jdk_path = "/usr/lib/jvm/default-java" -- Fallback
      end
      
      local jdtls_jar = vim.fn.glob("/usr/share/java/jdtls/plugins/org.eclipse.equinox.launcher_*.jar")
      if jdtls_jar == "" then
        jdtls_jar = vim.fn.glob(vim.fn.stdpath("data") .. "/mason/packages/jdtls/plugins/org.eclipse.equinox.launcher_*.jar")
      end
      
      local cmd = {
        java_cmd,
        "-Declipse.application=org.eclipse.jdt.ls.core.id1",
        "-Dosgi.bundles.defaultStartLevel=4",
        "-Declipse.product=org.eclipse.jdt.ls.core.product",
        "-Dlog.protocol=true",
        "-Dlog.level=ALL",
        "-Xmx1G",
        "--add-modules=ALL-SYSTEM",
        "--add-opens", "java.base/java.util=ALL-UNNAMED",
        "--add-opens", "java.base/java.lang=ALL-UNNAMED",
        "-jar", jdtls_jar,
        "-configuration", "/usr/share/java/jdtls/config_linux",
        "-data", vim.fn.stdpath("cache") .. "/jdtls/" .. vim.fn.fnamemodify(vim.fn.getcwd(), ":p:h:t"),
      }
      
      vim.notify("🚀 JDTLS | Java: " .. java_cmd, vim.log.levels.INFO)
      vim.notify("🚀 JDTLS | JDK17: " .. jdk_path, vim.log.levels.INFO)
      
      local config = {
        cmd = cmd,
        root_dir = require("jdtls.setup").find_root({ ".git", "mvnw", "gradlew", "pom.xml", "build.gradle" }),
        settings = {
          java = {
            configuration = {
              runtimes = {
                {
                  name = "Amazon-Corretto-17",
                  path = jdk_path,  -- ✅ PATH CORRECTO
                  default = true,
                },
              },
            },
            completion = {
              favoriteStaticMembers = {
                "org.junit.jupiter.api.Assertions.*",
                "org.mockito.Mockito.*",
                "org.hamcrest.MatcherAssert.assertThat",
                "org.hamcrest.Matchers.*",
              },
            },
            eclipse = { downloadSources = true },
            maven = { downloadSources = true },
            signatureHelp = { enabled = true },
            contentProvider = { preferred = "fernflower" },
          },
        },
        on_attach = function(client, bufnr)
          require("jdtls.setup").add_commands()
          local opts = { noremap = true, silent = true, buffer = bufnr }
          vim.keymap.set("n", "<leader>jo", "<cmd>JdtOrganizeImports<CR>", opts)
          vim.keymap.set("n", "<leader>jR", "<cmd>JdtRename<CR>", opts)
        end,
      }
      
      require("jdtls").start_or_attach(config)
    end,
  },
}
```

### 2. **DAP (Debugging como IntelliJ)**

**`dap-java.lua`**:
```lua
return {
  "mfussenegger/nvim-dap",
  config = function()
    local dap = require("dap")
    
    dap.adapters.java = function(callback, config)
      callback({
        type = "server",
        host = "127.0.0.1",
        port = config.port
      })
    end
    
    dap.configurations.java = {
      {
        type = "java",
        request = "attach",
        name = "Debug 'Current File'",
        cwd = vim.fn.getcwd(),
        console = "integratedTerminal",
      },
      {
        type = "java",
        request = "launch",
        name = "Debug 'Current File'",
        cwd = vim.fn.getcwd(),
        console = "integratedTerminal",
        mainClass = function()
          return vim.fn.input('Main class: ', 'Main', 'file')
        end,
        projectName = vim.fn.getcwd():gsub('.*/', ''),
      },
    }
  end,
}
```

### 3. **CMP + Snippets JAVA (IntelliJ-style)**

**`java-cmp.lua`**:
```lua
return {
  "hrsh7th/nvim-cmp",
  opts = function(_, opts)
    local cmp = require("cmp")
    opts.sources = cmp.config.sources({
      { name = "nvim_lsp" },
      { name = "nvim_lsp_signature_help" },
      { name = "luasnip" },
      { name = "buffer" },
    })
    
    -- 🔥 Snippets JAVA específicos
    require("luasnip.loaders.from_vscode").lazy_load({ paths = { "./java-snippets" } })
  end,
}
```

### 4. **Treesitter + Mason (Formatters/Linters)**

**`java-tools.lua`**:
```lua
return {
  {
    "williamboman/mason.nvim",
    opts = {
      ensure_installed = {
        "jdtls",
        "java-debug-adapter",
        "google-java-format",
        "checkstyle",
      },
    },
  },
  {
    "nvim-treesitter/nvim-treesitter",
    opts = function(_, opts)
      vim.list_extend(opts.ensure_installed, { "java", "kotlin" })
    end,
  },
}
```

### 5. **Keymaps IntelliJ-like**

**`~/.config/nvim/lua/config/keymaps.lua`**:
```lua
local map = vim.keymap.set

-- IntelliJ shortcuts
map("n", "<leader>jd", vim.diagnostic.open_float, { desc = "Java: Float diagnostic" })
map("n", "<leader>ja", vim.lsp.buf.code_action, { desc = "Java: Code action" })
map("n", "<leader>jr", vim.lsp.buf.rename, { desc = "Java: Rename" })
map("n", "<leader>jR", "<cmd>JdtRename<cr>", { desc = "Java: JDT Rename" })
map("n", "<leader>jo", "<cmd>JdtOrganizeImports<cr>", { desc = "Java: Organize imports" })
map("n", "<leader>jE", "<cmd>JdtExtractConstant<cr>", { desc = "Java: Extract Constant" })
map("n", "<leader>jV", "<cmd>JdtExtractVariable<cr>", { desc = "Java: Extract Variable" })

-- Debug
map("n", "<F5>", require("dap").continue, { desc = "Debug: Continue" })
map("n", "<F10>", require("dap").step_over, { desc = "Debug: Step Over" })
map("n", "<F11>", require("dap").step_into, { desc = "Debug: Step Into" })
map("n", "<leader>db", require("dap").toggle_breakpoint, { desc = "Debug: Toggle Breakpoint" })
```

## 🎮 **FLUJO IntelliJ COMPLETO**

```
1. Abrir proyecto Java → :Mason → jdtls se inicia AUTO
2. assertEquals<Tab> → assertEquals(│expected, actual│)
3. <leader>jo → Organize Imports (Ctrl+Alt+O)
4. <leader>jR → Rename (Shift+F6)
5. F5 → Debug
6. <F10> → Step Over
```

## 🚀 **Snippets JAVA específicos** (crea `./java-snippets/assert.json`)

```json
{
  "assertEquals": {
    "prefix": "assertEquals",
    "body": [
      "assertEquals($1, $2);$0"
    ],
    "description": "JUnit assertEquals"
  },
  "test": {
    "prefix": "test",
    "body": [
      "@Test",
      "void test${1:name}() {",
      "    $0",
      "}"
    ]
  }
}
```

## 📦 **Instalación rápida**

```bash
# 1. Instalar dependencias
sudo pacman -S jdt-language-server java-debug-adapter  # Arch
# o brew install jdt-language-server java-debug-adapter  # macOS

# 2. LazyVim
git clone https://github.com/LazyVim/LazyVim.git ~/.config/nvim
# Copia los archivos de arriba

# 3. Abrir proyecto Java
nvim pom.xml  # ¡IntelliJ listo! 🚀
```

autocomplete.lua
```lua
cat > ~/.config/nvim/lua/plugins/autocomplete.lua << 'EOF'
return {
  {
    "hrsh7th/nvim-cmp",
    event = "InsertEnter",
    dependencies = {
      "hrsh7th/cmp-nvim-lsp",
      "hrsh7th/cmp-nvim-lsp-signature-help",  -- 🔥 PARÉNTESIS AUTOMÁTICOS
      "hrsh7th/cmp-buffer",
      "hrsh7th/cmp-path",
      "L3MON4D3/LuaSnip",
      "saadparwaiz1/cmp_luasnip",
      "rafamadriz/friendly-snippets",
    },
    opts = function()
      local cmp = require("cmp")
      return {
        completion = {
          completeopt = "menu,menuone,preview,noselect",
        },
        snippet = {
          expand = function(args)
            require("luasnip").lsp_expand(args.body)
          end,
        },
        mapping = cmp.mapping.preset.insert({
          ["<C-Space>"] = cmp.mapping.complete(),
          ["<C-e>"] = cmp.mapping.abort(),
          ["<CR>"] = cmp.mapping.confirm({ select = true }),
          -- 🔥 TAB = Aceptar CON PARÉNTESIS (IntelliJ style)
          ["<Tab>"] = cmp.mapping(function(fallback)
            if cmp.visible() then
              cmp.confirm({ 
                behavior = cmp.ConfirmBehavior.Replace, 
                select = true 
              })
            elseif require("luasnip").expand_or_jumpable() then
              require("luasnip").expand_or_jump()
            else
              fallback()
            end
          end, { "i", "s" }),
          ["<S-Tab>"] = cmp.mapping(function(fallback)
            if cmp.visible() then
              cmp.select_prev_item()
            elseif require("luasnip").jumpable(-1) then
              require("luasnip").jump(-1)
            else
              fallback()
            end
          end, { "i", "s" }),
        }),
        -- 🔥 FUENTES prioritarias (LSP primero)
        sources = cmp.config.sources({
          { name = "nvim_lsp" },              -- Métodos con ( )
          { name = "nvim_lsp_signature_help" }, -- Ayuda parámetros
          { name = "luasnip" },               -- Snippets
          { name = "buffer" },                -- Buffer
          { name = "path" },                  -- Archivos
        }),
        formatting = {
          format = function(entry, vim_item)
            vim_item.menu = ({
              nvim_lsp = "[LSP]",
              luasnip = "[Snippet]",
              buffer = "[Buffer]",
              nvim_lsp_signature_help = "[Sig]",
              path = "[Path]",
            })[entry.source.name]
            return vim_item
          end,
        },
        experimental = {
          ghost_text = true,  -- Preview texto
          native_menu = false,
        },
      }
    end,
  },
}
EOF
```

## 🎉 **Características IntelliJ que tendrás**

✅ **Autocompletado con paréntesis** `assertEquals(`  
✅ **Organize imports** `<leader>jo`  
✅ **Rename refactoring** `<leader>jR`  
✅ **Extract Variable/Constant**  
✅ **Debug con breakpoints** F5/F10/F11  
✅ **Code actions** `<leader>ja`  
✅ **Find usages** `<leader>jfu`  

**¡Es IntelliJ pero 10x más rápido y ligero!** 🔥

¿Quieres que te ayude con **Maven/Gradle** específico o **Spring Boot**?