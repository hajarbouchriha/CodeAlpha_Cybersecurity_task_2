# CodeAlpha_Secure_Coding_Review
Task 2 summary: Completed a comprehensive Secure Coding Review for a PHP application, where I carefully analyzed the code to pinpoint and assess security vulnerabilities like Insecure Direct Object References (IDOR). Presented actionable suggestions to fortify secure coding practices and invite you to be part of our mission to build a secure online space for everyone!


Let's find out together what an IDOR is?

Insecure Direct Object References (or IDOR) is a simple bug that packs a punch. When exploited, it can provide attackers with access to sensitive data or passwords or give them the ability to modify information. IDORs cannot be detected by tools alone. IDORs require creativity and manual security testing to identify them. While some scanners might detect activity, it takes a human eye to analyze, evaluate, and interpret.

# Vulnerable Code:
The code retrieves a secret based on the provided "id" parameter without checking if the user is authorized to access that secret. An attacker can manipulate the id parameter to view secrets belonging to other users.
<?php

// Include the strip.php file from the _helpers directory
require_once('../_helpers/strip.php');

// Establish a connection to the SQLite database named 'test.db'
$db = new SQLite3('test.db');

// Retrieve the 'id' parameter from the GET request
$id = $_GET['id'];

// Check if 'id' parameter is provided
if (strlen($id) > 0) {
  
  // View a specific secret based on the provided 'id'
  // Note: Lack of authorization check allows any 'id' to be used, compromising security
  $query = $db->query('SELECT * FROM secrets WHERE id = ' . (int)$id);

  // Iterate through query results and display the content of the 'secret' column
  while ($row = $query->fetchArray()) {
    echo 'Secret: ' . $row['secret'];
  }

  // Provide a link to go back to the main page
  echo '<br /><br /><a href="/">Go back</a>';

} else {
  
  // View all secrets belonging to the user with 'user_id = 1'
  $query = $db->query('SELECT * FROM secrets WHERE user_id = 1');

  // Display heading for user's secrets
  echo '<strong>Your secrets</strong><br /><br />';

  // Iterate through query results and display links to individual secrets
  while ($row = $query->fetchArray()) {
    echo '<a href="/?id=' . $row['id'] . '">#' . $row['id'] . '</a><br />';
  }
}
?>
