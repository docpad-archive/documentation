1. Say you were to create the following website structure:
  
  > - myWebsite
    - src
      - documents
      - layouts
      - public

1. Install a few plugins:
  
  ```
  cd myWebsite
  npm install docpad-plugin-eco docpad-plugin-markdown
  ```

1. Create the following files:
    
  - A layout at `src/layouts/default.html.eco`, which contains
    
    ``` html
    <html>
      <head><title><%=@document.title%></title></head>
      <body>
        <%-@content%>
      </body>
    </html>
    ```

  - And another layout at `src/layouts/post.html.eco`, which contains:

    ``` html
    ---
    layout: default
    ---
    <h1><%=@document.title%></h1>
    <div><%-@content%></div>
    ```

  - And a document at `src/documents/posts/hello.html.md`, which contains:

    ``` html
    ---
    layout: post
    title: Hello World!
    ---
    Hello **World!**
    ```

1. Then when you generate your website with DocPad using `docpad run` you will get a html file at `out/posts/hello.html`, which contains:
  
  ``` html
  <html>
    <head><title>Hello World!</title></head>
    <body>
      <h1>Hello World!</h1>
      <div>Hello <strong>World!</strong></div>
    </body>
  </html>
  ```

1. And any files that you have in `src/public` will be copied to the `out` directory. E.g. `src/public/styles/style.css` -> `out/styles/style.css`

1. Allowing you to easily generate a website which only changes (and automatically updates) when a document changes (which when you think about it; is the majority of websites)

1. Cool, now what was with the `<%=...%>` and `<%-...%>` parts which were substituted away?
  
  - This is possible because we parse the documents and layouts through a template rendering engine. The template rendering engine used in this example was [Eco](https://github.com/sstephenson/eco) (hence the `.eco` extensions of the layouts). Templating engines allows you to do some pretty nifty things, in fact we could display all the titles and links of our posts with the following:
    
    ``` html
    <% for document in @documents: %>
      <% if document.url.indexOf('/posts') is 0: %>
        <a href="<%= document.url %>"><%= document.title %></a><br/>
      <% end %>
    <% end %>
    ```

1. Cool that makes sense... now how did `Hello **World!**` in our document get converted into `Hello <strong>World!</strong>`?
  
  - That was possible as that file was a [Markdown](http://daringfireball.net/projects/markdown/basics) file (hence the `.md` extension it had). Markdown is fantastic for working with text based documents, as it really allows you to focus in on your content instead of the syntax for formatting the document!

1. Great thanks! I think I will give it a go right now!

