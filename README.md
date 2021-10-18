# The Vooka Theme

[![Ghost version](https://img.shields.io/badge/Ghost->=3.x-brightgreen.svg)](https://github.com/TryGhost/Ghost)
[![Release](https://img.shields.io/github/release/tjbanks/Vooka-Theme.svg)](https://github.com/tjbanks/Vooka-Theme/)
[![GitHub forks](https://img.shields.io/github/forks/tjbanks/Vooka-Theme.svg)](https://github.com/tjbanks/Vooka-Theme/network)
[![GitHub stars](https://img.shields.io/github/stars/tjbanks/Vooka-Theme.svg?style=social&label=Star)](https://github.com/tjbanks/Vooka-Theme/stargazers)

Theme for Ghost :ghost:

## Installation
- [Stable Version](https://github.com/tjbanks/Vooka-Theme/releases/latest/)
- [Development Version](https://github.com/tjbanks/Vooka-Theme/tags/)

Download the `.zip` file and upload it at your Ghost Admin > Setting > Design.

## NEW Features

### The `hometags` post
Creating a post with the title `hometags` and adding tags to this post will show other posts categorized on the homepage based on the `hometags` tags. Only the primary tag will get selected for display on the homepage.

### Full-width iframe post template

Inserting something like the following as the only content on the page will result in a full width iframe.
```
<iframe width="100%" src="https://duckduckgo.com" style="height: 1000px"></iframe>
```

## Features and Usage

### Logo
If only **site icon** is uploaded, the Logo area will display the **icon** and followed by the **Site name** then a dot colored as the **main color**.

If **site logo** is uploaded, then the Logo area will only display the **site logo**. 

> Note: Since the top navbar is colored with white background, it would be better to use a dark/colorful logo.

### Assets Localization
You could customize the following files to define the CDN of assets to speed up access in specific regions: 
- `./default.hbs`
- `./partials/post/post_footer.hbs`
- `./partials/post/post_toc.hbs`

### Internal tags
Internal tags start with `#`, after creating it will displayed as internal tag automatically. Internal tags will not be displayed in front-end. So far the Vooka Theme support the following internal tags:
- **Carousel**: Use internal tag `#carousel`(slug:`hash-carousel`) to add posts into carousel in homepage (see [Showcase](#showcase)). 
- **No Index**: Use internal tag `#noindex`(slug:`hash-noindex`) to exclude posts from listing in home page. 
> limitation: hiding posts with `#noindex` tag, but the number of posts displayed for that page will change as well.

### Showcase
The showcase section is built to highlight posts. It is available only on the homepage. Insert the following code into Ghost Admin -> Code injection -> `Site Header` to enable the showcase:

```javascript
<script>
  var show_showcase = true; //default: false
</script>
```

The left slider carousel part detects the internal tag `#carousel`. The right part will display 2 featured posts.

### Author Page
You can customize the author page by editing your **profile** in Ghost Admin, such as **name**, **avatar**, **background image**, **social account links**, **location** and **bio**.

### Tag Page
You can customize the tag page by editing **tags** in Ghost Admin, such as **image**, **description**. 

### Custom Templates
Open the gear icon ⚙ while editing a post or page, scroll to the bottom and change `Template` option.

### Collection
To enable collection, edit the `routes.yaml` as below. Then modify the `home.hbs` to customize your homepage. Full doc: [Ghost Docs - Collections](https://docs.ghost.org/api/handlebars-themes/routing/collections/)

```yaml
routes:
  /: home # template for homepage `home.hbs`

collections:
  /movie/: # a collection called movie
    permalink: /movie/{slug}/
    template: movie # template `movie.hbs`
    filter: tag:movie # fetch data from a tag:movie
    data: tag.movie # have access to all data & meta data from tag
  /music/: # a collection called music
    permalink: /music/{slug}/
    template: music # template `music.hbs`
    filter: primary_tag:music # fetch data from primary tag: music
    data: tag.music # have access to all data & meta data from tag
```

> **Notice**: known issues of Ghost collection, e.g.: [Ghost #10082](https://github.com/TryGhost/Ghost/issues/10082).

### Custom CSS Variables
Download the theme `.zip` file, unzip it then edit the variables in `assets/css/custom.css` to customize your theme coloring. After that, zip everything back into a `.zip` file and upload it onto your Ghost admin.

### Custom Footer Text
By default, your **site description** (Ghost Admin -> General) will be displayed in the footer text. If you need to change it, define a variable `footer_text` in the `Site Header` as below:

```javascript
<script>
  var footer_text = "REPLACE WITH YOUR FOOTER TEXT HERE";
</script>
```
> You can include HTML in the `footer_text`, but be careful to use single quotation marks inside it. For example:
> `var footer_text = "REPLACE <span style='color:red;font-weigh'>WITH</span> YOUR FOOTER TEXT HERE <i class='iconfont icon-heart'></i>";`

### :speech_balloon: Comment System
Ghost itself doesn't have a comment system, we need to use third party solutions for this. Some options are: [DISQUS][disqus], [Gitalk][gitalk], [Valine][valine] and [Vssue][vssue]. By default, Vooka has Gitalk and DISQUS integrated. Skip the following if you do not need the comment system.

**By default, the comment system is disabled.** To enable it, first insert the following code into `Post Header` for a single post or `Site Header` for the whole site at Ghost Admin -> Code injection to configure accordingly, then choose one of the comment systems below and follow the instruction.

```javascript
<script>
  var show_comment = true; //default: false
</script>
```

#### Gitalk (Recommended)
Gitalk is a Github issue based comment system. Automatically support `en`, `zh_CN`, `zh_TW`, `es` by detecting the language of user's navigator.
1. Register a new **GitHub Application**
2. Create a new **Github Repository** for your website
3. Insert the following code into Ghost Admin -> Code injection: `Site Footer`, and modify the configuration with your **Github App** & **Repository** from previous steps.

```javascript
<script>
  const gitalk = new Gitalk({
    clientID: 'GitHub Application Client ID',
    clientSecret: 'GitHub Application Client Secret',
    repo: 'GitHub repo',
    owner: 'GitHub repo owner',
    admin: ['GitHub repo owner and collaborators, only these guys can initialize github issues'],
    id: location.pathname,      // Ensure uniqueness and length less than 50
    distractionFreeMode: false  // Facebook-like distraction free mode
  });
  gitalk.render('gitalk-container');
</script>
```
> more usage guide and options please check [here](https://github.com/gitalk/gitalk#usage).


#### DISQUS
Insert the following code into Ghost Admin -> Code injection: `Site Header`, and modify the link with yours.
```javascript
<script>
    var disqus_link = 'https://YOURLINK.disqus.com/embed.js'; // change it with your DISQUS js link
</script>
```
If you want to change the comment system, you need to modify the code in `partial/post/post_comment.hbs`.

###  Code Highlight
Prism.js is used for syntax highlighting, the default languages and plugins used by Vooka theme are:
  - **Languages**: Markup (e.g. HTML), CSS, C-like, JavasScript, Bash, Nginx, Ruby, Git, JSON, Markdown, SQL, Python, R
  - **Plugins**: line-numbers, toolbar, show-language.

To customize this yourself, open [customize Prismjs][custom-prism] and choose the languages you need. Then download the js and css files to overwrite the `prism.js` and `prism.css` files in `assets` folder.

#### Line-numbers
The line numbers are hidden by default. To enable it, insert the following code into `Post Header` for a single post or `Site Header` for the whole site:
```js
<script>
  var line_numbers = true; //default: false
</script>
```

### TOC
There are two ways to control the TOC of a post:
1. insert the following code into `Post Header` for a single post or `Site Header` for the whole site;
    ```javascript
    <script>
        var show_toc = true; // enable TOC (default: false)
    </script>
    ```
2. Use custom post template `Post With Toc` to enable TOC. 
> **Priority**: `template` > `Post Header` > `Site Header`

> **Notice**: h2 and h3 headings on the page will be displayed by default. If you want to add other headings (e.g. h1 or h4), please edit `selectors` of the file `partials/post/post_toc.hbs`. However, you should not use h1 except for the post title.

### Instant Search
The search function uses Ghost Content API. To enable it (added to top menu), first add a custom integration in Ghost Admin. Then copy the **Content API Key** and **API URL**.
Go to the Code injection, add the following code to the `Site Header`:
```javascript
<script>
  var show_search = true; // default:false
  var search_key = 'PASTE THE CODE YOU COPIED AS Content API Key';
  var search_url = 'PASTE THE CODE YOU COPIED AS API URL'; // it is usually your site url
</script>
```

### LaTeX support
Use `$`(inline) or `$$` to cover commands to render for LaTeX commands.

### Link Page
Create a link page is nothing different than create a normal page. With the **Bookmark Card** feature since Ghost v2.30, you can easily add links to any page by type `/bookmark` in Ghost editor. 

### Components
- **Navigation**: You can modify `partials/navigation.hbs` to customize your dropdown menu, or delete the section if not needed.
- **Badge**: include `class="badge <color>"` to use badge (HTML only).
  - Supported colors: uncolored, red, yellow, green, blue, purple
![image](https://user-images.githubusercontent.com/40261916/64512333-bcb27a80-d318-11e9-8b60-1f18468e3a30.png)
    > Note: to use uncolored badge, set as `class="badge"`.
- **Posts per page**: change the number of `"posts_per_page": 8` in `package.json`
- **table**: to unwrap cells, uncomment the `/* white-space: nowrap; */` in `assets/css/main.css` around **line 703**.

### Credit
If you want to disable the top right "Get Vooka Theme" button, insert the following code into your `Site Header` from `Code Injection`:

```javascript
<script>
  var vooka_credit = false; // default:true
</script>
```

## Changelog

See [CHANGELOG.md](./CHANGELOG.md)

## Contributors

See [Contributors][contributors]

## Dependencies

- [Bulma][bulma] - CSS Framework
- [Prismjs][prismjs] - A lightweight syntax highlighter
- [JQuery][jquery] - A well-known JavaScript library (for tocify only now)
- [jQuery.tocify.js][tocify] - Table of Content generator (also JQuery-UI)
- [KaTeX][katex] - A faster LaTeX equation rendering library (since v0.3.0)
- [Gitalk][gitalk] - A Github issued based comment system (since v0.3.0)
- [ghost-search][ghost-search] - An instant search library using Ghost Content API (since v1.0.0)
- [iconfont][iconfont] - A free icon solution (since v1.2.3)

## Roadmap
To know the future planning of this project, please visit our [Roadmap][roadmap].

## Bug Report & :dart: Features Request
If you find a bug, thinking about something to be improved or even want new features, please feel free to post an issue. 

Alternatively you could contribute to this project.

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b feature-fooBar`)
3. Commit your changes (`git commit -m 'Add something'`)
4. Push to the branch to origin (`git push origin feature-fooBar`)
5. Create a new Pull Request to `dev` branch here
6. Wait for code review and modify if necessary

## Original Fork

https://github.com/huangyuzhang/Fizzy-Theme


[bulma]: https://bulma.io/
[prismjs]: https://prismjs.com/
[jquery]: https://jquery.com/
[tocify]: http://gregfranko.com/jquery.tocify.js/
[mathjax]: https://www.mathjax.org/
[katex]: https://katex.org/
[disqus]: https://disqus.com/
[gitalk]: https://github.com/gitalk/gitalk
[valine]: https://github.com/xCss/Valine
[vssue]: https://github.com/meteorlxy/vssue
[custom-prism]: https://prismjs.com/download.html#themes=prism-tomorrow&languages=markup+css+clike+javascript+bash+ruby+git+json+markdown+nginx+sql+python+r&plugins=line-numbers+toolbar+show-language
[ghost-search]: https://github.com/HauntedThemes/ghost-search
[iconfont]:https://www.iconfont.cn