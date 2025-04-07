# Global-connections
Vendemos futuro
import { useState } from "react";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { ShoppingCart, Instagram } from "lucide-react";
import { motion } from "framer-motion";

const products = [
  // ... mismos productos que antes
];

const amazonLinks = [
  // ... mismos enlaces de Amazon que antes
];

export default function Storefront() {
  const [cart, setCart] = useState([]);
  const [selections, setSelections] = useState({});
  const [search, setSearch] = useState("");
  const [filterStorage, setFilterStorage] = useState("");
  const [filterColor, setFilterColor] = useState("");

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
    if (!selected.storage || !selected.color)
      return alert("Selecciona almacenamiento y color");
    setCart([...cart, { ...product, ...selected }]);
  };

  const filteredProducts = [...products, ...amazonLinks].filter((product) => {
    const matchesSearch = product.name.toLowerCase().includes(search.toLowerCase());
    const matchesStorage = filterStorage ? product.storage.includes(filterStorage) : true;
    const matchesColor = filterColor ? product.colors.includes(filterColor) : true;
    return matchesSearch && matchesStorage && matchesColor;
  });

  return (
    <div className="min-h-screen bg-white text-black px-4 py-6 md:px-12">
      <header className="flex justify-between items-center mb-10">
        <h1 className="text-3xl font-semibold">iPhone Store</h1>
        <div className="flex items-center gap-4">
          <a href="https://instagram.com/tu_tienda" target="_blank" rel="noopener noreferrer">
            <Instagram className="w-6 h-6 hover:text-blue-500" />
          </a>
          <ShoppingCart className="w-6 h-6" />
          <span className="text-sm">{cart.length} productos</span>
        </div>
      </header>

      <div className="mb-6 grid grid-cols-1 md:grid-cols-3 gap-4">
        <input
          type="text"
          placeholder="Buscar modelo..."
          value={search}
          onChange={(e) => setSearch(e.target.value)}
          className="border px-3 py-2 rounded w-full"
        />
        <select
          value={filterStorage}
          onChange={(e) => setFilterStorage(e.target.value)}
          className="border px-3 py-2 rounded w-full"
        >
          <option value="">Filtrar por almacenamiento</option>
          <option value="64GB">64GB</option>
          <option value="128GB">128GB</option>
          <option value="256GB">256GB</option>
          <option value="512GB">512GB</option>
          <option value="1TB">1TB</option>
        </select>
        <select
          value={filterColor}
          onChange={(e) => setFilterColor(e.target.value)}
          className="border px-3 py-2 rounded w-full"
        >
          <option value="">Filtrar por color</option>
          <option value="Negro">Negro</option>
          <option value="Blanco">Blanco</option>
          <option value="Rojo">Rojo</option>
          <option value="Azul">Azul</option>
          <option value="Dorado">Dorado</option>
          <option value="Gris espacial">Gris espacial</option>
          <option value="Verde">Verde</option>
        </select>
      </div>

      <section className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
        {filteredProducts.map((product) => (
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
                <Button onClick={() => addToCart(product)} className="w-full">
                  Añadir al carrito
                </Button>
              </CardContent>
            </Card>
          </motion.div>
        ))}
      </section>

      <section className="mt-12">
        <h3 className="text-2xl font-semibold mb-4">También disponibles por encargo</h3>
        <p className="text-sm text-gray-600">
          Todos los modelos están disponibles por encargo. Escríbenos por Instagram para más detalles.
        </p>
      </section>
    </div>
  );
}
