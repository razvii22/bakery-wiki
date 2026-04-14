<ul>
    {%- for page in site.pages -%}
        {%- if page.title -%}
            <h2 id="{{page.title}}">{{page.title}}</h2>
            <li><a href="{{page.url | relative_url}}">{{page.path}}</a></li>
            <hr>
        {%- endif -%}
    {%- endfor -%}
</ul>
