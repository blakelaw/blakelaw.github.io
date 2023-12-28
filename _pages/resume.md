---
layout: archive
title: "Résumé"
permalink: /resume/
author_profile: true
redirect_from:
  - /resume
---

<html>
<head>
    <meta charset="UTF-8">
    <title>Résumé</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Responsive Styles -->
    <style>
        @media screen and (max-width: 768px) {
            .resume-embed {
                width: 100%;
                height: auto; /* Adjust this as needed */
            }
        }

        @media screen and (min-width: 769px) {
            .resume-embed {
                width: 480px;
                height: 400px;
            }
        }
    </style>
</head>
<body>

{% include base_path %}

<hr class="light-grey-line">

<!-- Download link for the PDF -->
<a href="https://blakelaw.dev/files/BlakeLawResume.pdf" download="Blake_Law_Resume.pdf">Click here</a> to download.
<br><br>

<!-- Embedded PDF with responsive class -->
<embed class="resume-embed" src="https://blakelaw.dev/files/BlakeLawResume.pdf" type="application/pdf" />

</body>
</html>
