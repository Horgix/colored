# Colored

[![Build
Status](https://travis-ci.org/mackwic/colored.svg?branch=master)](https://travis-ci.org/mackwic/colored) [![Crates.io](https://img.shields.io/crates/v/colored.svg?maxAge=2592000)](https://crates.io/crates/colored) [![Crates.io](https://img.shields.io/crates/l/colored.svg?maxAge=2592000)](https://github.com/mackwic/colored/blob/master/LICENSE)

Coloring terminal so simple, you already know how to do it !

```rust
    "this is blue".blue();
    "this is red".red();
    "this is red on blue".red().on_blue();
    "this is also red on blue".on_blue().red();
    "you can also make bold comments".bold();
    println!("{} {} {}", "or use".cyan(), "any".italic().yellow(), "string type".cyan());
    "or change advice. This is red".yellow().blue().red();
    "or clear things up. This is default color and style".red().bold().clear();
    "purple and magenta are the same".purple().magenta();
    "you can specify color by string".color("blue").on_color("red");
    "and so are normal and clear".normal().clear();
    String::from("this also works!").green().bold();
    format!("{:30}", "format works as expected. This will be padded".blue());
    format!("{:.3}", "and this will be green but truncated to 3 chars".green());
```

## How to use

Add this in your `Cargo.toml`:

```toml
[dependencies]
colored = "1.5"
```

and add this to your `lib.rs` or `main.rs`:

```rust
    extern crate colored;

    use colored::*;

    // test the example with `cargo run --example most_simple`
    fn main() {
        // TADAA !
        println!("{} {} !", "it".green(), "works".blue().bold());
    }
```

## Features

- Safe rust, easy to use, minimal dependencies, complete test suite
- Respect the `CLICOLOR`/`CLICOLOR_FORCE` behavior (see [the specs](http://bixense.com/clicolors/))

#### Colors:

- black
- red
- green
- yellow
- blue
- magenta (or purple)
- cyan
- white

Background colors: prepend the color by `on_`. Simple as that.

#### Styles:

- bold
- underline
- italic
- dimmed
- reversed
- blink
- hidden

You can clear color _and_ style anytime by using `normal()` or `clear()`

#### Advanced Control:

##### Dynamic color from str

As `Color` implements `FromStr`, `From<&str>`, and `From<String>`, you can easily cast a string into a color like that:

```rust
// the easy way
"blue string yo".color("blue");

// this will default to white
"white string".color("zorglub");

// the safer way via a Result
let color_res = "zorglub".parse(); // <- this returns a Result<Color, ()>
"red string".color(color_res.unwrap_or(Color::Red));
```


##### Colorization control

If you want to disable any coloring at compile time, you can simply with using
the `no-color` feature.

For example, you can do this in your `Cargo.toml` to disable color in tests:

```toml
[features]
# this effectively enable the feature `no-color` of colored when testing with
# `cargo test --feature test`
test = ["colored/no-color"]
```

You can use have even finer control by using the `colored::control::should_colorize` methods.

## Todo

- **Windows console support**: this works only with ansi term. I plan to support
  the windows console also.
- **More tests ?**: We always wecome more tests ! Please contribute !

## Credits

This library wouldn't have been the same without the marvelous ruby gem [colored](https://github.com/defunkt/colored).

Thanks for the [ansi\_term crate](https://github.com/ogham/rust-ansi-term) for
providing a reference implementation, which greatly helped making this crate
output correct strings.

## Licence

Mozilla Public Licence 2.0. See the LICENCE file at the root of the repository.

In non legal terms it means that:
- if you fix a bug, you MUST give me the code of the fix (it's only fair)
- if you change/extend the API, you MUST give me the code you changed in the
  files under MPL2.
- you CAN'T sue me for anything about this code
- appart from that, you can do almost whatever you want. See the LICENCE file
  for details.

## Contributors

- Thomas Wickham: [@mackwic](https://github.com/mackwic)
- Corey "See More" Richardson: [@cmr](https://github.com/cmr)
- Iban Eguia: [@Razican](https://github.com/Razican)
