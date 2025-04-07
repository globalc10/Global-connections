import { useState } from "react";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { ShoppingCart, Instagram } from "lucide-react";
import { motion } from "framer-motion";

const products = [
  {
    id: 1,
    name: "iPhone 13 Pro",
    price: "$999",
    image: "/iphone13pro.jpg",
    storage: ["128GB", "256GB", "512GB"],
    colors: ["Grafito", "Plateado", "Dorado", "Sierra Blue"],
  },
  {
    id: 2,
    name: "iPhone 14",
    price: "$1099",
    image: "/iphone14.jpg",
    storage: ["128GB", "256GB", "512GB"],
    colors: ["Rojo", "Blanco estelar", "Negro medianoche", "Azul"],
  },
  {
    id: 3,
    name: "iPhone 15 Pro Max",
    price: "$1399",
    image: "/iphone15promax.jpg",
    storage: ["256GB", "512GB", "1TB"],
    colors: ["Titanio natural", "Titanio azul", "Titanio blanco", "Titanio negro"],
  },
  {
    id: 7,
    name: "iPhone Xs",
    price: "$499",
    image: "/iphonexs.jpg",
    storage: ["64GB", "256GB", "512GB"],
    colors: ["Gris espacial", "Plateado", "Dorado"],
  },
  {
    id: 8,
    name: "iPhone Xr",
    price: "$449",
    image: "/iphonexr.jpg",
    storage: ["64GB", "128GB"],
    colors: ["Blanco", "Negro", "Azul", "Coral", "Rojo"],
  },
  {
    id: 9,
    name: "iPhone 11",
    price: "$499",
    image: "/iphone11.jpg",
    storage: ["64GB", "128GB", "256GB"],
    colors: ["Negro", "Verde", "Amarillo", "Malva", "Rojo", "Blanco"],
  },
  {
    id: 10,
    name: "iPhone 11 Pro",
    price: "$699",
    image: "/iphone11pro.jpg",
    storage: ["64GB", "256GB", "512GB"],
    colors: ["Gris espacial", "Plateado", "Oro", "Verde noche"],
  },
  {
    id: 11,
    name: "iPhone 12",
    price: "$799",
    image: "/iphone12.jpg",
    storage: ["64GB", "128GB", "256GB"],
    colors: ["Negro", "Blanco", "Rojo", "Verde", "Azul", "Morado"],
  },
  {
    id: 12,
    name: "iPhone 12 Pro",
    price: "$899",
    image: "/iphone12pro.jpg",
    storage: ["128GB", "256GB", "512GB"],
    colors: ["Gris espacial", "Plateado", "Dorado", "Azul pacífico"],
  },
  {
    id: 13,
    name: "iPhone SE 2022",
    price: "$429",
    image: "/iphonese2022.jpg",
    storage: ["64GB", "128GB", "256GB"],
    colors: ["Negro", "Blanco", "Rojo"],
  },
];

const amazonLinks = [
  {
    id: 4,
    name: "iPhone 11 (Renovado)",
    price: "$399",
    image: "/iphone11.jpg",
    url: "https://www.amazon.com/dp/B08N5WRWNW",
    storage: ["64GB", "128GB"],
    colors: ["Negro", "Blanco", "Verde", "Amarillo", "Malva", "Rojo"]
  },
  {
    id: 5,
    name: "iPhone XR (Renovado)",
    price: "$349",
    image: "/iphonexr.jpg",
    url: "https://www.amazon.com/dp/B07P6Y7954",
    storage: ["64GB", "128GB"],
    colors: ["Blanco", "Negro", "Azul", "Coral", "Rojo"]
  },
  {
    id: 6,
    name: "iPhone SE 2020 (Renovado)",
    price: "$299",
    image: "/iphonese2020.jpg",
    url: "https://www.amazon.com/dp/B093TKYDRQ",
    storage: ["64GB", "128GB"],
    colors: ["Negro", "Blanco", "Rojo"]
  },
];

export default function Storefront() {
  const [cart, setCart] = useState([]);
  const [selections, setSelections] = useState({});

  const handleSelect = (id, type, value) => {
    setSelections((prev) => ({
      ...prev,
      [id]: {
        ...prev[id],
        [type]: value,
      },
    }));
  };

  const addToCart = (product) => {
    const selected = selections[product.id] || {};
    if (!selected.storage || !selected.color) {
      return alert("Selecciona almacenamiento y color");
    }
    setCart([...cart, { ...product, ...selected }]);
  };

  const removeFromCart = (id) => {
    setCart(cart.filter(item => item.id !== id));
  };

  const clearCart = () => {
    setCart([]);
  };

  return (
    <div className="min-h-screen bg-white text-black px-4 py-6 md:px-12">
      <header className="flex justify-between items-center mb-10">
        <h1 className="text-3xl font-semibold">iPhone Store</h1>
        <div className="flex items-center gap-4">
          <a href="https://instagram.com/tu_tienda" target="_blank" rel="noopener noreferrer">
            <Instagram className="w-6 h-6 hover:text-blue-500" />
          </a>
          <div className="flex items-center gap-2">
            <ShoppingCart className="w-6 h-6" />
            <span className="text-sm">{cart.length} productos</span>
          </div>
        </div>
      </header>

      <section className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
        {[...products, ...amazonLinks].map((product) => (
          <motion.div
            key={product.id}
            whileHover={{ scale: 1.03 }}
            className="transition-all"
          >
            <Card className="rounded-2xl shadow-md hover:shadow-lg">
              <CardContent className="p-4">
                <img
                  src={product.image}
                  alt={product.name}
                  className="w-full h-48 object-cover rounded-xl mb-4"
                />
                <h2 className="text-xl font-medium mb-1">{product.name}</h2>
                <p className="text-gray-700 mb-1">{product.price}</p>
                <div className="mb-2">
                  <label className="block text-sm mb-1">Almacenamiento:</label>
                  <select
                    className="w-full border rounded px-2 py-1"
                    onChange={(e) => handleSelect(product.id, "storage", e.target.value)}
                    value={selections[product.id]?.storage || ""}
                  >
                    <option value="">Selecciona</option>
                    {product.storage.map((option) => (
                      <option key={option} value={option}>{option}</option>
                    ))}
                  </select>
                </div>
                <div className="mb-2">
                  <label className="block text-sm mb-1">Color:</label>
                  <select
                    className="w-full border rounded px-2 py-1"
                    onChange={(e) => handleSelect(product.id, "color", e.target.value)}
                    value={selections[product.id]?.color || ""}
                  >
                    <option value="">Selecciona</option>
                    {product.colors.map((color) => (
                      <option key={color} value={color}>{color}</option>
                    ))}
                  </select>
                </div>
                {product.url && (
                  <a
                    href={product.url}
                    target="_blank"
                    rel="noopener noreferrer"
                    className="block text-blue-500 text-sm mb-2 hover:underline"
                  >
                    Ver en Amazon
                  </a>
                )}
                <Button
                  onClick={() => addToCart(product)}
                  className="w-full"
                  disabled={!selections[product.id]?.storage || !selections[product.id]?.color}
                >
                  Añadir al carrito
                </Button
