# blogs


## Contents

- [About Jekyll](#about-jekyll)
- [How to install/run](#how-to-installrun)
- [Options/Usage](#optionsusage)
  - [Header navigation links](#header-navigation-links)
  - [Footer links](#footer-links)
  - [Copyrights/Disclaimer statements](#copyrightsdisclaimer-statements)
- [License](#license)

## About jekyll 

[Jekyll](http://jekyllrb.com/) is a static site generator, an open-source tool for creating simple yet powerful websites of all shapes and sizes.

## How to install/run

1. Clone it: git clone https://github.com/udacity/panda.
2. If you completely new to jekyll, please read more about [Jekyll](http://jekyllrb.com/) and [Github pages](https://help.github.com/articles/using-jekyll-with-pages).
3. Change your directory into cloned repository. 
4. Run `bundle install`
5. Edit the _config.yml on root directory. Change `url` property to to 
`http://127.0.0.1:4000` since you are going to run on localhost.
6. Run the jekyll server by having: `bundle exec jekyll serve`   

Try to locate your browser at [http://localhost:4000](http://localhost:4000).

Note: If you are a windows user please refer this nice website - http://jekyll-windows.juthilo.com/ by Julian Thilo to configure ruby + jekyll on windows.

### Includes 

All the partial includes are under `_includes` directory.

#### Header navigation links

Feel free to add/edit links for your header in the file `header-links.html`.

#### Footer links

Customize your footer links by editing `_includes/footer-links.html`

#### Copyrights/Disclaimer statements

All the copyrights notes are under `_includes/footer.html`. Also note that you 
can toggle on/off copyright note from front-end by setting up `show_disclaimer` 
property in `_config.yml`. 

## License

The original code is from https://github.com/web-create/harmony under [MIT](https://github.com/web-create/harmony/blob/master/LICENSE.md) License.
