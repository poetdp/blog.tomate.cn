- /layout/post.ejs

```html
<!-- Copyright Widget -->
<div style="margin:1pc auto;min-width: 90%;padding:1pc;">
    <br><br><hr><p style="color: grey"><em>本站所有文章均已在版权印备案，如需转载或为他用请访问版权印。</em> <span style="display:inline-block;"><a target="_blank" href="http://101703100005299.bqy.pub" style="color:pink;">获取授权</a></span></p><p style="color: grey"></p>
</div>

<!-- Donate Widget -->
<iframe src="http://rocjzh.coding.me/donate-widget/" height=250px frameborder="0"></iframe>
```

- /layout/partial/footer.ejs

```html
<!--Copyright-->
<div id="copyright">
    Copyright&nbsp;©&nbsp;
    <script type="text/javascript">
        var fd = new Date();
        document.write(fd.getFullYear());
    </script>
    &nbsp;<a target="_blank" href="https://github.com/rocj">DINGPENG</a><!--<%- config.title %>-->
</div>

<div class="mdl-mini-footer--right-section">
    <div>
        <div class="footer-develop-div">皖 ICP 备 <a target="_blank" href="http://ahcainfo.miitbeian.gov.cn">17012372</a> 号</div>
    </div>
</div>
```

- source/img

- source/404.html

- source/fonts