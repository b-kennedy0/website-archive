---
layout: page
---
<html lang="en-GB">
 <body>
    <ul>
       {% for emails in site.emails %}
            {% if emails.name contains '.md' or emails.name contains '.html' %}
                <li><a href="{{ site.baseurl }}{{ emails.url }}">{{ emails.url }}</a></li>
            {% endif %}
        {% endfor %}
    </ul>
</body>
</html>
    
