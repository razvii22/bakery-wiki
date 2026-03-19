<ul>
    {%- for page in site.pages -%}
        {%- if page.title -%}
            <li><a href="{{page.url | relative_url}}">{{page.path}}</a></li>
            <hr>
        {%- endif -%}
    {%- endfor -%}
</ul>