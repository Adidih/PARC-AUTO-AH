<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Disponibilité des véhicules</title>
<style>
body {font-family: Arial; text-align:center; background:#f2f2f2;}
table {margin:auto; border-collapse:collapse; width:90%; background:white;}
th, td {border:1px solid #ccc; padding:10px;}
th {background:#333; color:white;}
.dispo {background:green; color:white;}
.occupe {background:red; color:white;}
</style>
</head>
<body>

<h1>Disponibilité des véhicules</h1>

<table id="fleetTable">
<tr>
<th>Véhicule</th>
<th>Chauffeur</th>
<th>Téléphone</th>
<th>Statut Jour</th>
<th>Statut Nuit</th>
</tr>
</table>

<script src="https://cdnjs.cloudflare.com/ajax/libs/Tabletop.js/1.5.1/tabletop.min.js"></script>
<script>
var publicSpreadsheetUrl = 'LIEN_DE_TA_FEUILLE_PUBLIQUE_ICI';

function init() {
  Tabletop.init({
    key: publicSpreadsheetUrl,
    simpleSheet: true,
    callback: showInfo
  });
}

function showInfo(data, tabletop) {
  const table = document.getElementById('fleetTable');
  // Supprimer toutes les lignes sauf l'en-tête
  table.querySelectorAll('tr:not(:first-child)').forEach(tr => tr.remove());

  data.forEach(item => {
    const tr = document.createElement('tr');
    tr.innerHTML = `
      <td>${item.Véhicule}</td>
      <td>${item.Chauffeur}</td>
      <td>${item.Téléphone}</td>
      <td class="${item['Statut jour'] === 'Disponible' ? 'dispo' : 'occupe'}">${item['Statut jour']}</td>
      <td class="${item['Statut nuit'] === 'Disponible' ? 'dispo' : 'occupe'}">${item['Statut nuit']}</td>
    `;
    table.appendChild(tr);
  });
}

window.addEventListener('DOMContentLoaded', init);
</script>

</body>
</html>
