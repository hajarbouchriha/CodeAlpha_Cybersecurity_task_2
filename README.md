# CodeAlpha_Secure_Coding_Review
Task 2 summary: Completed a comprehensive Secure Coding Review for a PHP application, where I carefully analyzed the code to pinpoint and assess security vulnerabilities like Insecure Direct Object References (IDOR). Presented actionable suggestions to fortify secure coding practices and invite you to be part of our mission to build a secure online space for everyone!


Let's find out together what an IDOR is?

Insecure Direct Object References (or IDOR) is a simple bug that packs a punch. When exploited, it can provide attackers with access to sensitive data or passwords or give them the ability to modify information. IDORs cannot be detected by tools alone. IDORs require creativity and manual security testing to identify them. While some scanners might detect activity, it takes a human eye to analyze, evaluate, and interpret.

# Vulnerable Code:
The code retrieves a secret based on the provided "id" parameter without checking if the user is authorized to access that secret. An attacker can manipulate the id parameter to view secrets belonging to other users.
