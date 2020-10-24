<script context="module" lang="ts">
    export async function preload(page, session) {
        const { slug } = page.params;

        const res = await this.fetch(
            `https://article.api.zackmyers.io/v1/articles/slug/${slug}`
        );
        const article = await res.json();

        const res_auth = await this.fetch(
            `https://user.api.zackmyers.io/v1/users/${BigInt(
                article.author_id
            )}`
        );
        const author = await res_auth.json();

        return { article, author };
    }
</script>

<script lang="ts">
    import marked from "marked";
    import hljs from "highlight.js";
    import dayjs from "dayjs";
    import relativeTime from "dayjs/plugin/relativeTime";
    import {decode} from "js-base64";

    export let article: string, author: string;

    let str = decode(article.body);
    dayjs.extend(relativeTime);
    let time = dayjs(article.created_at).fromNow();

    const renderer = new marked.Renderer();

    renderer.code = (source: string, lang: string) => {
        const { value: highlighted } = hljs.highlight(lang, source);
        return `<pre class="code p-5 rounded-lg my-3 overflow-x-auto"><code>${highlighted}</code></pre>`;
    };

    renderer.heading = (text: string, level: number) => {
        let scales = [
            {
                level: 0,
                name: "text-4xl"
            },
            {
                level: 1,
                name: "text-xl"
            },
            {
                level: 2,
                name: "text-lg"
            }
        ];

        let className: string;
        for (let i: number = 0; i < scales.length; i++) {
            if (scales[level-1]) {
                className = scales[level-1].name;
            }
        }

        return `<h${level} class="${className} py-3 font-bold">${text}</h${level}>`;
    }

    renderer.paragraph = (text: string) => {
        return `<p class="text-lg py-3">${text}</p>`;
    }

    const html = marked(str, { renderer });
</script>

<svelte:head>
    <title>{`${article.title} - Zack Myers Blog`}</title> 
</svelte:head>

<div class="px-12 flex flex-col items-center dark-bg">
    <div class="mt-24 text-gray-500 uppercase text-sm font-semibold tracking-wide">{`By ${author.name}`}</div>
    <div class="text-cool-gray-100 text-4xl font-extrabold">{article.title}</div>
    <div class="text-gray-500 font-semibold">{time}</div>
    <div class="mt-24 p-6 sm:px-12 border border-gray-800 rounded-3xl shadow-xl text-gray-300 block max-w-xs sm:max-w-lg md:max-w-3xl lg:max-w-5xl">
        <div class="">{@html html}</div>
    </div>
</div>

<style>
    div {
        font-family: 'Inter';
    }

    .dark-bg {
        background:#101113;
    }
</style>