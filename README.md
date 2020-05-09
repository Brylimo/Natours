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
2. npm  
    >($)npm init  
    >($)npm install node-sass --save-dev    // installed as devDependencies(tool for the development)  
    
3. live-server  
    It automaticlly detects whether the source code files have changed and implements them without reloading.
    * npm install live-server -g (install live-server globally)
    >($) live-server  
  
4. npm run compile:sass  
    In the package.json file, we can set the "scripts" part as   
    "compile:sass": "node-sass sass/main.scss css/style.css -w"  
    
    ->(name of the package) (input file) (output file) -w // if we set -w flag here,  
    whenever we change something on the Sass code, it automatically reflects them on the css code.  
    >($) npm run compile:sass    
  
5. 7-1 pattern  
: 7 folders & 1 main Sass file
    * partial files are started with underscore. eg) "\_base.scss"
    * import partial files using _@import_ in main Sass file.
    * You should not put underscore and .scss when you import partial files to main Sass file. eg) '@import "base/base"' 
    
6. GRID practice  
    1. max-width  
       :If we have enough available space, then it will have the width that we've specified. However, if there's not enough width,
       then it will simply fill 100% of the available space that it has.  
       
    2. &:not(:last-child) {...}   
       :Without ":not", it will simply select the last child. What it does here is opposite of this action.  
       So, basically, we select everything except last child.  
       
    3. calc()  
       :Calculation function but we can mix units while using it.  
       -> You gotta use #{Sass variable} when you want to use Sass variables  
       
    4. [alt="logo"] {...}  
       :It selcets all of the elements which have this alt attribute equal to "logo".  
       
7. About section  
    1. \<main\> tag   
        :this is one of the HTML5 elements that tells search engines or screen readers that this is the real main part of our site.  
        It will contain most of the website components.  
    
    2. Emmet  
        :Extension that you can install in your text editor. It allows you to write HTML a lot faster and easier.  
        eg) \<div\> tag -> '.' + class name and 'tab' / \<section\> tag -> 'section.section-about' + 'tab'  
        
    3. background-clip: text;  
        :background is clipped exactly where the text is.  
        It's a new thing in CSS so it needs -webkit- prefix. Thus, <code>-webkit-background-clip: text;</code>    
        
    4. Special symbols/characters for HTML5  
        ->codingheroes: https://css-tricks.com/snippets/html/glyphs/  
        
    5. Outline related CSS properties    
        * outline    
        :makes outline to the element.  
        
        * outline-offset  
        :this property will give space between the outline and element that the outline is applied.  
        
8. Features section  
    1. icon(https://linea.io/)  
        Download All Icons -> \_basic -> \_ICONFONT -> Copy fonts folder and styles.css(icon-font.css)  
        (You can refer how it looks like by icons-reference.html)  
        * icon font is also a text
        * scalable
        * different formats files are in the 'fonts folder'  
        
        <code><link rel="stylesheet" href="css/icon-font.css></code> 
    
    2. child selector  
    :하위 요소 전체에 스타일을 적용하는 것이 아니라 자식 요소에만 스타일을 적용할 수 있다.  
    <code>parent element > child element</code>  
    
9. Tours section  
    1. Photos(https://unsplash.com/)  
    
    2.  background-blend-mode  
    :It makes gradient or colors blend with images.  
    It's also a new added thing in CSS so it isn't applied in Internet Explorer browser.  
    <code>background-blend-mode: screen;</code>  
    
    3. box-decoration-break   
    :문장 잘라졌을 때 서로 다른걸로 인식시켜줘서 따로따로 패딩이 가능하게 함.  
    <code>box-decoration-break: clone;</code>  
    
10. Stories section  
    1. shape-outside property  
    :uses vectorize shape here like clip-path property / float and height, width property are essential to use this property  
    -> 주변 글자나 파트들을 지정된 모양으로 element를 둘러싸도록 만든다.  
    eg) shape-outside: circle(50% at 50% 50%) // (radius of the circle, at focus position)  
    
    2. filter  
    :필터링 속성 적용  
    eg) <code>filter: blur(3px) brightness(80%);</code>  
    
    3. Videos(https://coverr.co)   
    mp4, webm -> adaptable to almost all browsers    
    
    4. <code>object-fit: cover;</code>  
    :pretty similar to <code>background-size: cover</code>  
    element(video in this case) fills the entire parent while still maintaining its aspect ratio.  
    (It works with HTML elements or videos.)  
