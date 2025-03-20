from flask import Flask, render_template_string, redirect

app = Flask(__name__)

# HTML template for the homepage
homepage_html = """
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Custom Cloudflare App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f5f5f5;
        }
        .reviews {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 20px;
        }
        .review {
            width: 150px;
            height: 150px;
            background-color: #ddd;
            border-radius: 10px;
        }
        .button {
            margin-top: 20px;
            padding: 10px 20px;
            background-color: #28a745;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .button:hover {
            background-color: #218838;
        }
    </style>
</head>
<body>
    <h1>Simple Cloudflare App</h1>
    <p>See what others are saying about us!</p>
    <div class="reviews">
        <div class="review">Review 1</div>
        <div class="review">Review 2</div>
        <div class="review">Review 3</div>
    </div>
    <button class="button" onclick="window.location.href='/menu'">Browse Options</button>
</body>
</html>
"""

# HTML template for the menu
menu_html = """
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Menu</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f5f5f5;
        }
        .menu {
            margin-top: 50px;
        }
        .menu button {
            display: block;
            margin: 10px auto;
            padding: 10px 20px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .menu button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <h1>Select an Option</h1>
    <div class="menu">
        <button onclick="window.location.href='/form/custom-bot'">Custom Bot</button>
        <button onclick="window.location.href='/form/custom-server'">Custom Server</button>
        <button onclick="window.location.href='/form/custom-bot-and-server'">Custom Bot and Server</button>
    </div>
</body>
</html>
"""

@app.route('/')
def homepage():
    return render_template_string(homepage_html)

@app.route('/menu')
def menu():
    return render_template_string(menu_html)

@app.route('/form/<option>')
def google_form(option):
    # Redirect to a Google Form based on the option selected
    google_forms = {
        "custom-bot": "https://docs.google.com/forms/d/e/1FAIpQLSe-example-form-url-1/viewform",
        "custom-server": "https://docs.google.com/forms/d/e/1FAIpQLSe-example-form-url-2/viewform",
        "custom-bot-and-server": "https://docs.google.com/forms/d/e/1FAIpQLSe-example-form-url-3/viewform"
    }
    return redirect(google_forms.get(option, '/'))

if __name__ == '__main__':
    app.run(debug=True)
