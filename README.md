<?php
// Sample PHP code for a simple Point of Sale (POS) system

class Product {
    public $name;
    public $price;

    public function __construct($name, $price) {
        $this->name = $name;
        $this->price = $price;
    }
}

class POS {
    private $products = [];
    private $cart = [];

    public function addProduct($product) {
        $this->products[] = $product;
    }

    public function addToCart($productName, $quantity) {
        foreach ($this->products as $product) {
            if ($product->name === $productName) {
                $this->cart[] = ['product' => $product, 'quantity' => $quantity];
                return;
            }
        }
        echo "Product not found.\n";
    }

    public function checkout() {
        $total = 0;
        echo "Receipt:\n";
        foreach ($this->cart as $item) {
            $product = $item['product'];
            $quantity = $item['quantity'];
            $subtotal = $product->price * $quantity;
            echo "{$product->name} x {$quantity} = $subtotal\n";
            $total += $subtotal;
        }
        echo "Total: $total\n";
    }
}

// Usage
$pos = new POS();
$pos->addProduct(new Product("Apple", 1.00));
$pos->addProduct(new Product("Banana", 0.50));

$pos->addToCart("Apple", 3);
$pos->addToCart("Banana", 2);

$pos->checkout();
?>
