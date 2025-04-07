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
    image: "/
