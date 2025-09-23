```js
class Product {
    private id: number
    private name: string
    private cost: number
    public constructor(id: number, name: string, cost: number) {
        this.id = id
        this.name = name
        this.cost = cost
    }
    public getName(): string {
        return this.name
    }
    public getCost(): number {
        return this.cost
    }
    public getId(): number {
        return this.id
    }
}
class ShoppingCart {
    private static instance: undefined | ShoppingCart
    private products: Product[]
    private constructor() {
        this.products = []
    }
    public add(product: Product): void {
        this.products.push(product)
    }
    public deleteById(id: number): void {
        this.products = this.products.filter(product => product.getId() !== id)
    }
    public getProducts(): Product[] {
        return this.products
    }
    public static getInstance(): ShoppingCart {
        if (!ShoppingCart.instance) ShoppingCart.instance = new ShoppingCart()
        return ShoppingCart.instance
    }
}
function clientApp() {
    const silla = new Product(1, 'Silla de oficina', 10000)
    const mesa = new Product(2, 'Mesa para oficina', 20000)
    const lampara = new Product(3, 'Lampara de oficina', 5000)
    const shoppingCart = ShoppingCart.getInstance()
    // agregamos los productos al carrito
    shoppingCart.add(silla)
    shoppingCart.add(mesa)
    shoppingCart.add(lampara)
    console.log(shoppingCart.getProducts())
    // eliminamos un producto
    shoppingCart.deleteById(mesa.getId())
    console.log(shoppingCart.getProducts())
}
clientApp()
```