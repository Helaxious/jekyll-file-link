## File Link
## What is `File link`?

`jekyll-file-link` is a Jekyll tag plugin to effortlessly link your post assets, cutting as much of unnecessary typing as possible.

Because the plugin removes all the boilerplate you need to write. Linking a file is as simple as just writing the *file name*:

```
{% file_link your_image_here.png %}
```

## How it works?

`jekyll-file-link` works by looking in the assets folder for something called the post folder, it's a folder where you store your post assets, each post should have one post folder. And they need to have the same name, excluding the date.

For example If my post's file is named:

```
1970-01-01-python-tips-and-tricks.md
```

Then my folder's going to be named:

```
python-tips-and-tricks
```

Make sure that you name it *exactly* like that.

So when you link a file:

```
{% file_link image.png %}
```

First, the plugin checks if there's a similar folder structure of the post, in the assets folder, in other words, if the post is in this path:

```
_posts/
  --/jekyll
    --/my-cool-post.md
```

`jekyll-file-link` will check if exists a folder in this path:

```
assets/
  --/jekyll
    --/my-cool-post <-- This is the post folder!
      --/image.png
```

If it exists, it returns the folder's path with the file name.

But if it doesn't find the folder, the plugin will do an automatic search looking in the assets directory for that folder, if it finds, it returns its path with the file name.

## How do I use it?

### How to organize your project

Although this plugin automatically searches for your files, it does require a bit of a *strict* folder structure

#### The `_posts` folder

For the `_posts` folder, you just need to make sure that you're not organizing your posts by date, because of the way this plugin searches folders, but if you're organizing your posts in categories, like `python`, `tutorials`, `games`, you're fine.

#### The assets folder

As for the assets folder, by default, the assets folder's name is `assets`, but you're able to set a different folder for your post's assets, you'll just need to specify the name of the folder in the `post_assets_folder` variable in `_config.yml`:

```yaml
post_assets_folder: "post_assets"
```
#### Grouping the post folders

You're also able to group your post folders into categories, just make sure that you don't include any categories that don't belong to the post:

```
# Post path
_posts/
  --/tutorials <-- categories
    --/jekyll <-- categories
      --/2022-03-20-jekyll-tutorial-1.md

# Assets path
assets/
  --/tutorials <-- categories
    --/jekyll <-- categories
      --/jekyll-tutorial-1 <-- The post folder
        --/jekyll-new-blog.gif
```

But that doesn't mean that you need to follow exactly the post's folder's structure, you just can't include any categories that the post doesn't have.

So if you have for example your assets like this:

```
assets/
  --/jekyll-tutorial-1 <-- The post folder
```

Or maybe like this:

```
assets/
  --/tutorials
    --/jekyll-tutorial-1 <-- The post folder
```

Or, for some reason, even like this:

```
assets/
  --/jekyll
    --/tutorials
      --/jekyll
        --/tutorials
          --/jekyll-tutorial-1 <-- The post folder
```

`jekyll-file-link` will still detect your asset and successfully link your file.

But if you prefer, you also can specify on the front matter its path:

```
---
assets: cool_folder
---
```

The plugin will not do a automatic search and just return `assets/cool_folder/your_image.png`

### Linking a file

Because of the preparation we have done, linking a file is now trivially easy, just write it like this:

```
{% file_link your-image-here.png %}
```

If your file is in a subfolder, just specify it as usual!

```
{% file_link img/your-image-here.png %}
```

If you do need to link an file that is outside of the post folder, you'll need to use the `link` tag:

```
{% link /path/to/your/file.ext %}
```

## Installation

(This plugin is still in a very early stage, later changes may *break completely* the functionality, please be certain that you want to use this plugin.)

Add `jekyll-file-link` in your `Gemfile`:

```
gem "jekyll-file-link"
```

And add `jekyll-file-link` in the `plugins` sections in your `_config.yml`:

```
plugins:
  - jekyll-file-link
  - jekyll-feed
```

Run `bundle` or install the gem with `gem install jekyll-file-link`

## What about [`jekyll-postfiles`?](https://github.com/nhoizey/jekyll-postfiles)

`jekyll-postfiles` is an awesome plugin, I would recommend it to everyone that uses jekyll, but I don't think it fits for my needs, as my blog is very image-heavy, I prefer to have a separate `post_assets` folder.

If your blog isn't file-heavy, and you don't frequently link files that often, you'll probably want `jekyll-postfiles` instead.

## Does it work with Github Pages?

Since Github Pages only allows a select few plugins, no, but if you set-up [`jekyll-deploy-action`](https://github.com/jeffreytse/jekyll-deploy-action), you're able to run any custom plugins (even this one) in your project.

## License

This plugin is licensed under the MIT license
