# SMACSS Guidelines
Scalable and Modular Architecture for CSS. It's not a library nor a framework. It's a guide that teaches you how to write your CSS. It's used to help you write maintanable and understandable stylesheets for your projects.

1. Use CSS classes for your selectors
2. CSS classes should have semantic meaning
3. You should be able to look at class names and know what a module does
4. Modules should be designed without context

**Advantages:**
* Easily understand your your CSS months after you complete a project
* Onboarding is easier since new hires can easily find the parts of a page to modify

### Base
These are your base styles where you define the default stylings for certain elements or classes on a page. You would add your CSS resets in this file**Layout rules should not be applied here**.

### Layout
Defines the basic layout for the major elements of your site (Header, Footer, Container, etc...). Grid systems would be applied here.

### Modules
*Modules* are defined as the reusable components of your site. These can be a button, an article section, a login form, etc... These can be used on more than one page ogf your site.

### State
A *state* is defined as a class that controls how a module looks when it's in a certain "state". E.g. Collapsible accordion, tab, a form error. These classes are added using JavaScript and react based on a user's actions.

### Themes
A *theme* is where you define the overall look of your site. In WordPress this would be your "front-page", "search results page", "post" page.

## SMACSS USING SCSS
![SMACSS SCSS folder structure](https://raw.githubusercontent.com/rxnlabs/smacss-guidelines/master/images/smacss-scss-folder-structure.png "SCSS folder structure for Newseum NYE using SMACSS")
### Examples
#### Base
##### _base.scss

```scss
@import 
"vendor/modularized-normalize-scss/normalize"
;
html,
body{
    color: $grey;
    font-size: $default_font_size;
    background: url('../images/bkg.jpg') #000 repeat;
    font-family: Georgia, "Times New Roman", serif;
    line-height: 1.6;
}

h1{
    color: $gold;
    font-family: 'com4t_drifylight';
    font-size: 2.3rem;
    font-weight: normal;
    padding-left: 6px;
    line-height: 1;
}

h2{
    color: $gold;
    font-weight: normal;
}

a:link{
    color: $gold;
    text-decoration: none;
}

img{
    height: auto;
    max-width: 100%;
}

.wrapper{
    background: #161310;
}

.flexslider{
    background: transparent!important;
    border: none!important;
    border-radius: 0!important;
}

main{
    padding: 0 5.4rem;
}

ul{
    list-style-position: inside;
    padding-left: 2rem;
}

footer{
    padding: 2rem 0;
    border-top: 2px solid;
    margin-top: 3rem;
    padding: 1.3rem 0px;
    font-size: .9rem;
}

.disclaimer{
    font-size: 90%;
    font-style: italic;
}
```
#### Layout
##### _layout.scss

```scss
@import 
"vendor/susy/sass/susy"
;
header,
footer{
    @include clearfix;
}

.container {
    @include container;
}

.wrapper{
    width: 100%;

    @include susy-media($desktop-large){
        max-width: 1000px;
        margin: 0 auto;
    }

    @include susy-media($desktop $desktop-large){
        width: 950px;
        margin: 0 auto;
    }

    @include susy-media($tablet $desktop){
        width: 850px;
        margin: 0 auto;
    }

    @include susy-media($phone $tablet){
        width: 750px;
        margin: 0 auto;
    }

}

main{
    @include susy-media(max-width $phone) {
        padding-left: 10px;
        padding-right: 10px;
    }
}
```
#### Modules
##### _modules.scss
```scss
.faq{
    &.is-collapsed{
        .faq-arrow{
            @include rotate(0deg);
        }
    }

    &.is-shown{
        .faq-arrow{
            @include animation-name(spin);
            @include rotate(90deg);
            @include animation-duration(2s);
            @include animation-timing-function(ease);
        }
    }

    .faq-arrow{
        position: relative;
        top: 5px;
        height: 24px;
    }

    .faq-link{
        cursor: pointer;
    }

    .faq-answer{
        margin-left: 28px;
    }
}

a.cta{
    @include linear-gradient(to right, #DCB044 0%, #F4C75E 42%);
    text-align: center;
    padding: 0.5rem 3rem 0rem;
    display: inline-block;
    border-radius: 10px;
    text-decoration: none;
    color: #000;
    font-size: 1.9rem;
    -webkit-box-shadow: 3px 3px 5px 0px rgba(50, 50, 50, 0.49);
    -moz-box-shadow:    3px 3px 5px 0px rgba(50, 50, 50, 0.49);
    box-shadow:         3px 3px 5px 0px rgba(50, 50, 50, 0.49);
    font-family: 'bignoodletitlingregular', sans-serif;

    &:hover,
    &:focus,
    &:active{
        color: #fff;
    }
}

.module{

    @include module();
    
    img{
        display: block;
        &:hover{
            opacity: 0.7;
        }
    }
    .title-background{
        background: transparentize(#000, .7);
        background-image: url('../images/module-footer.jpg');
        background-repeat: repeat;
        background-size: cover;
    }

    .title{
        padding: .8rem .5rem;
        margin: 0 auto;
        height: 34px;
    }
}
```
#### State
#### _state.scss
```scss
.is-collapsed{
    .content{
        display: none;
    }
}

.is-shown{
    .content{
        display: block;
    }
}
```
#### Theme
##### _tikets.scss
```scss
body.page-template-page-ticket{
    ul{
        padding-left: 0;

        li{
            margin-bottom: 5px;
        }
    }

    .price-button{
        margin-right: 1rem;
    }

    .ticket-container{
        @include clearfix;

        .ticket-price{
            @include span(4);
        }
    }
}
```
##### _front-page.scss
.page-template-front-page{

    .flexslider{
        margin-bottom: 20px;

        .flex-next{
            right: 0;
        }
    }
    
    .modules{
        @include clearfix;
        position: relative;
        top: -20px;

        .module{
            margin-top: 0.5rem;
            
            @include susy-media(min-width $phone){
                @include span(8);
                background: transparent;
                border: none;

                &:first-child,
                &:nth-child(4){
                    margin-left: -0.8rem;
                    margin-right: 1.4rem;
                }

                .inner{
                    @include module();
                }
                
                &:nth-child(3n),
                &:last-child{
                    @include span(8 of 24 last);
                    margin-right: -0.8rem;
                }
            }

            @include susy-media(min-width $desktop-large){
                .title{
                    font-size: 1.4rem;
                }
            }

            @include susy-media($desktop $desktop-large){
                .title{
                    font-size: 1.4rem;
                }
            }

            @include susy-media($phone $tablet){

                margin: 0;
                
                @include span(12 of 24);
                
                .title{
                    font-size: 1.3rem;
                }

                &:nth-child(3n),
                &:last-child{
                    @include span(12 of 24 last);
                    float: left;
                }
                
                &:first-child,
                &:nth-child(4){
                    margin-right: gutter(24);
                    margin-left: 0;
                }

                &:nth-child(even){
                    @include span(12 of 24 last);
                }
            }
        }
    }
}
```