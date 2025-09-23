```sh
sudo apt install zsh git
chsh -s $(which zsh)
#Otra alternativa es:
#chsh -s `which zsh`

```

Instalamos Oh My ZSH
```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

# Instalamos plugins 🔨

1. Los paquetes que vamos a instalar son:
    
    - **zsh-syntax-highlighting:** Si estas escribiendo los comando correctos en la terminal, les pone colores
```sh
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf && ~/.fzf/install
```
en nano ~/.zshrc

```.zshrc
plugins=(
git
zsh-syntax-highlighting
zsh-autosuggestions
)
```


**Fuente nerd**  
[![11](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fi%2Flhm015flg8geprwrpjd0.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fi%2Flhm015flg8geprwrpjd0.png)

1. Descargar una fuente con soporte para iconos.
    - Mi recomendación es descargar la fuente de [https://www.nerdfonts.com/font-downloads](https://www.nerdfonts.com/font-downloads)
    - La fuente que uso es la de JetBrainsMono Nerd Font

powerlvl10k
```sh
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

```txt
ZSH_THEME="powerlevel10k/powerlevel10k"
POWERLEVEL10K_MODE="nerdfont-complete"
```

```sh
p10k configure
```

