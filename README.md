from flask import Flask, jsonify, request

app = Flask(__name__)

# Simulazione di dati utente e post
users = [
    {"id": 1, "username": "user1", "email": "user1@example.com"},
    {"id": 2, "username": "user2", "email": "user2@example.com"}
]

posts = [
    {"id": 1, "user_id": 1, "content": "Hello, World!"},
    {"id": 2, "user_id": 2, "content": "This is a test post."}
]

# Endpoint per ottenere tutti gli utenti
@app.route('/users', methods=['GET'])
def get_users():
    """
    Restituisce tutti gli utenti registrati nel social network.

    Returns:
        list: Lista di dizionari rappresentanti gli utenti.
    """
    return jsonify(users)

# Endpoint per ottenere tutti i post
@app.route('/posts', methods=['GET'])
def get_posts():
    """
    Restituisce tutti i post pubblicati nel social network.

    Returns:
        list: Lista di dizionari rappresentanti i post.
    """
    return jsonify(posts)

# Endpoint per creare un nuovo utente
@app.route('/users', methods=['POST'])
def create_user():
    """
    Crea un nuovo utente nel social network.

    Request Body:
        dict: Dizionario rappresentante i dettagli del nuovo utente.

    Returns:
        dict: Dizionario rappresentante i dettagli del nuovo utente creato.
    """
    new_user = request.json
    users.append(new_user)
    return jsonify(new_user), 201

# Endpoint per creare un nuovo post
@app.route('/posts', methods=['POST'])
def create_post():
    """
    Crea un nuovo post nel social network.

    Request Body:
        dict: Dizionario rappresentante i dettagli del nuovo post.

    Returns:
        dict: Dizionario rappresentante i dettagli del nuovo post creato.
    """
    new_post = request.json
    posts.append(new_post)
    return jsonify(new_post), 201

if __name__ == '__main__':
    app.run(debug=True)
