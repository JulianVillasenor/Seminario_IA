# Seminario_IA

En este repositorio se desarrollara el avance sobre el proyecto de seminario de inteligencia artificial.
El proyecto sera un sistema de recomendaciones, para esto se necesitaran obtener o generar datos para realizar entrenamiento y pruebas de prediccion para el sistema de recomendaciones.   

import random
import pandas as pd

### Categorías y productos
categories = {
    "pizzas": ["Margherita", "Pepperoni", "Hawaiana", "Veggie", "Marinara"],
    "hamburguesas": ["Clásica", "Cheeseburger", "BBQ Burger", "Veggie Burger"],
    "appetizers": ["Alitas", "Nachos", "Aros de Cebolla", "Dedos de Queso"],
    "postres": ["Tarta de Chocolate", "Cheesecake", "Helado", "Brownie"],
    "cafes": ["Latte", "Espresso", "Cappuccino", "Americano"],
    "bebidas": ["Refresco", "Agua", "Jugo Natural"],
    "tragos": ["Margarita", "Mojito", "Piña Colada"],
    "cervezas": ["IPA", "Pale Ale", "Lager", "Stout"]
}

### Generar productos
products = []
product_id = 1
for category, items in categories.items():
    for item in items:
        products.append({
            "item_id": product_id,
            "category": category,
            "name": item,
            "price": round(random.uniform(5, 20), 2),
            "popularity": round(random.uniform(0.1, 1), 2),
            "calories": random.randint(100, 800)
        })
        product_id += 1

### Generar usuarios
users = [
    {
        "user_id": user_id,
        "age": random.randint(18, 60),
        "gender": random.choice(["M", "F"]),
        "preferences": random.sample(list(categories.keys()), k=random.randint(2, 4))
    }
    for user_id in range(1, 21)
]

### Generar interacciones
interactions = []
for _ in range(100):  # Generar 100 interacciones
    user = random.choice(users)
    item = random.choice(products)
    interactions.append({
        "user_id": user["user_id"],
        "item_id": item["item_id"],
        "rating": random.randint(1, 5),
        "timestamp": pd.Timestamp.now()
    })

### Convertir a DataFrames
products_df = pd.DataFrame(products)
users_df = pd.DataFrame(users)
interactions_df = pd.DataFrame(interactions)

### Guardar como CSV
products_df.to_csv("productos.csv", index=False)
users_df.to_csv("usuarios.csv", index=False)
interactions_df.to_csv("interacciones.csv", index=False)

print("Datos generados y guardados como CSV.")

