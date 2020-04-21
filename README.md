# Natours
Advanced CSS and Sass

## Techniques included
 
1. Sass  
    Sass is a CSS preprocessor, an extension of CSS that adds power and elegance to the basic language.  
    Sass source code ->(Sass compiler)-> Compiled CSS code
    
    Main Sass features
    * Variables: for reusable values such as colors, font-sizes, spacing, etc.
    * Nesting: to nest selectors inside of one another, allowing us to write less code.
    * Operators: for mathematical operations right inside of CSS.
    * Partials and imports: to write CSS in different files and importing them all into one single file.
    * Mixins: to wirte reusable pieces off CSS code.
    * Functions: similar to mixins, with the difference that they produce a value that can be used.
    * Extends: to make different selectors inherit declarations that are common to all of them.
    * Control directives: for writing complex code using conditionals and loops.
    
    ### EXAMPLE(nav bar)
    ```shell
    <!--html-->
    <nav class="clearfix">
        <ul class="navigation">
            <li><a href="#">About us</a></li>
            <li><a href="#">Pricing</a></li>
            <li><a href="#">Contact</a></li>
        </ul>
        <div class="button">
            <a class="btn-main" href="#">Sign up</a>
            <a class="btn-hot" href="#">Get a quote</a>
        </div>
    </nav>
    ```
    
    
    ```shell
    // SCSS
    * {
      margin: 0;
      padding: 0;
    }

    $color-primary: #f9ed69; //yellow
    $color-secondary: #f08a5d;
    $color-tertiary: #b83b5e;
    $color-text-dark: #333;
    $color-text-light: #eee;

    $width-button: 150px;

    @mixin clearfix {
      &::after {
        content: "";
        clear: both;
        display: table;
      }  
    }

    @mixin style-link-text($col) {
      text-decoration: none;
      text-transform: uppercase;  
      color: $col;
    }

    @function divide($a, $b) {
      @return $a / $b;
    }

    nav {
      margin: divide(60, 2) * 1px; //30px
      background-color: $color-primary;

      @include clearfix;
    }

    .navigation {
      list-style: none;
      float: left;

      li {
        display: inline-block;
        margin-left: 30px;

        &:first-child { //.navigation li:first-child
          margin: 0;
        }

        a:link {
          @include style-link-text($color-text-dark);
        }
      }
    }

    .button {
      float: right;
    }

    %btn-placeholder { //이 자리에 .btn-main:link가 온다. mixin과의 차이점
      padding: 10px;
      display: inline-block;
      text-align: center;
      border-radius: 100px;
      width: $width-button;
      @include style-link-text($color-text-light);
    }

    .btn-main {
      &:link {
        @extend %btn-placeholder;
        background-color: $color-secondary;
      }
      &:hover {
        background-color: darken($color-secondary, 15%);
      }
    }

    .btn-hot {
      &:link {
        @extend %btn-placeholder;
        background-color: $color-tertiary;
      }
      &:hover {
        background-color: lighten($color-tertiary, 10%);
      }
    }
    ```
2. live-server  
    It automaticlly detects whether the source code files have changed and implements them without reloading.
    * npm install live-server -g (install live-server globally)
    >($) live-server  