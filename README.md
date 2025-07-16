# how-to-get-rich
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Bankdaten Eingeben</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        label { display: block; margin-top: 10px; }
        input { width: 300px; padding: 5px; }
        .success { color: green; margin-top: 20px; }
        a { display: block; margin-top: 20px; }
    </style>
</head>
<body>
    <h1>Bankdaten eingeben</h1>
    <form id="bankForm">
        <label for="name">Name:</label>
        <input type="text" id="name" required>

        <label for="iban">IBAN:</label>
        <input type="text" id="iban" required>

        <label for="bic">BIC:</label>
        <input type="text" id="bic" required>

        <br><br>
        <button type="submit">Speichern</button>
    </form>

    <div class="success" id="successMessage"></div>

    <a href="anzeige.html">Gespeicherte Daten anzeigen</a>

    <script>
        document.getElementById('bankForm').addEventListener('submit', function(e) {
            e.preventDefault();

            const name = document.getElementById('name').value;
            const iban = document.getElementById('iban').value;
            const bic = document.getElementById('bic').value;

            const daten = { name, iban, bic };
            localStorage.setItem('bankdaten', JSON.stringify(daten));

            document.getElementById('successMessage').textContent = "✅ Daten wurden gespeichert!";
            this.reset();
        });
    </script>
</body>
</html>
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <title>Gespeicherte Bankdaten</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 40px; }
        .daten { margin-top: 20px; }
        a { display: block; margin-top: 20px; }
    </style>
</head>
<body>
    <h1>Gespeicherte Bankdaten</h1>
    <div class="daten" id="ausgabe"></div>

    <a href="index.html">Zurück zur Eingabe</a>

    <script>
        const daten = localStorage.getItem('bankdaten');
        const ausgabe = document.getElementById('ausgabe');

        if (daten) {
            const obj = JSON.parse(daten);
            ausgabe.innerHTML = `
                <strong>Name:</strong> ${obj.name}<br>
                <strong>IBAN:</strong> ${obj.iban}<br>
                <strong>BIC:</strong> ${obj.bic}
            `;
        } else {
            ausgabe.textContent = "Keine Daten gespeichert.";
        }
    </script>
</body>
</html>
