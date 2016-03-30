## Hacksmiths Food Project API Docs

## Getting Started
This site uses middleman, a static site generator.  It uses [Slate](https://github.com/tripit/slate) to generate the documentation website.  In order to edit it, please see the [index.html.md](https://github.com/teamhacksmiths/food-drivr-api-documentation/blob/master/source/index.html.md) file.  It will parse Markdown into the HTML seen on the website.  Please follow the [Slate documentation](https://github.com/tripit/slate) if the below instructions do not work for you.

### Prerequisites

You're going to need:

 - **Linux or OS X** — Windows may work, but is unsupported.
 - **Ruby, version 1.9.3 or newer**
 - **Bundler** — If Ruby is already installed, but the `bundle` command doesn't work, just run `gem install bundler` in a terminal.

### Getting Set Up

1. Fork this repository on Github.
2. Clone *your forked repository* (not our original one) to your hard drive with `git clone https://github.com/YOURUSERNAME/slate.git`
3. `cd slate`
4. Initialize and start Slate. You can either do this locally, or with Vagrant:

```shell
# either run this to run locally
bundle install
bundle exec middleman server

# OR run this to run with vagrant
vagrant up
```

You can now see the docs at http://localhost:4567. Whoa! That was fast!

Now that Slate is all set up your machine, you'll probably want to learn more about [editing Slate markdown](https://github.com/tripit/slate/wiki/Markdown-Syntax), or [how to publish your docs](https://github.com/tripit/slate/wiki/Deploying-Slate).

If you'd prefer to use Docker, instructions are available [in the wiki](https://github.com/tripit/slate/wiki/Docker).

## Built With
* [Slate](https://github.com/tripit/slate)

## Authors

* **Ryan Collins**

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments
