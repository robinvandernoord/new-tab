<script>
    export let article;

    function strip_html(text) {
        return text.replace(/(<([^>]+)>)/gi, "");
    }

    function ellipse(text, len) {
        if (text.length > len - 3) {
            text = text.slice(0, len) + '...';
        }

        return text;
    }

    let body = ellipse(
        strip_html(article.body || "").replace('\n', '<br/><br/>')
        , 500);
</script>

<style>
    img {
        max-width: 100%;
    }

    h3 {
        font-size: 2em;
        padding: 10px;
    }

    p {
        font-size: 1.5em;
        padding: 10px;
    }

    a {
        all: unset;
    }
</style>

<a href="https://news.su6.nl/read?id={article.id}">
    <h3>{article.title}</h3>
    <img src="{article.image}" />
    <p>{@html body}</p>
</a>