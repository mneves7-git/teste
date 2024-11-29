import sqlite3

def create_table():
    conn = sqlite3.connect('inventory.db')
    c = conn.cursor()
    c.execute('''CREATE TABLE IF NOT EXISTS products (
                    id INTEGER PRIMARY KEY,
                    name TEXT,
                    category TEXT,
                    quantity INTEGER,
                    price REAL,
                    location TEXT)''')
    conn.commit()
    conn.close()

def add_product(name, category, quantity, price, location):
    conn = sqlite3.connect('inventory.db')
    c = conn.cursor()
    c.execute("INSERT INTO products (name, category, quantity, price, location) VALUES (?, ?, ?, ?, ?)",
              (name, category, quantity, price, location))
    conn.commit()
    conn.close()
    print(f'Produto {name} adicionado com sucesso!')

def view_products():
    conn = sqlite3.connect('inventory.db')
    c = conn.cursor()
    c.execute("SELECT * FROM products")
    products = c.fetchall()
    conn.close()
    for product in products:
        print(product)

if __name__ == '__main__':
    create_table()
    while True:
        print("1. Adicionar Produto")
        print("2. Ver Produtos")
        choice = input("Escolha uma opção: ")
        
        if choice == '1':
            name = input("Nome do Produto: ")
            category = input("Categoria: ")
            quantity = int(input("Quantidade: "))
            price = float(input("Preço: "))
            location = input("Localização no Depósito: ")
            add_product(name, category, quantity, price, location)
        
        elif choice == '2':
            view_products()
        
        else:
            print("Opção inválida!")
