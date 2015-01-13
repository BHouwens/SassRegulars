# Setup of the CSS

The `style.scss` file in this folder is the core file that imports all others into it. It's also the file that the Sass gem should watch and build a source map out of. There are two folders, base and layout, which contain the Sass partials from which the final stylesheet is made. Base contains all of the functionality for the stylesheets, such as functions and mixins, while layout contains all the partials that deal with specific elements or types of elements in the HTML.

The .sass-cache folder is simply a cache of previous compiles to get the gem to compile quickly going forward. It's generated automatically by the Sass gem.

The folder `css/docs` contains the documentation for Sass functions, mixins etc in the `index.html` file.

## Source Map

The `styles.css.map` is a source map of the main stylesheet. It maps every rule to its original Sass partial file (so classes declared in `_nav.scss` are mapped as such, for example). Keep this in the folder only for development purposese, as Chrome is able to use the source map to make debugging with DevTools much easier (inspect any element and DevTools will display its source as its Sass file instead of the compiled CSS).

## Quick rundown of Sass terms

Just a quick rundown so that the partials in the base folder make sense:

###Placeholder 

Used in Sass to group recurring statements together. These can then be used throughout the stylesheet, and the compiled result will concatenate all the occurences together so that there's no repetition.

Example:

    %placeholder{
    	display: block;
    	color: white;
    	font-weight: bold;
    }  

    .foo{
    	@extend %placeholder;
    }

    .bar{
    	@extend %placeholder;
    }

Compiled result:

	.foo, .bar{
		display: block;
		color: white;
		font-weight: bold;
	}


###Mixin

More-or-less the same as a placeholder, only it accepts arguments like a function. Possibly the most useful thing in Sass

Example:

	@mixin size($width, $height){
		display: block;
		width: $width;
		height: $height;
	}

	.foo{
		@include size(40px, 50px);
	}

	.bar{
		@include size(60px, 200px);
	}

Result:

	.foo{
		display: block;
		width: 40px;
		height: 50px;
	}

	.bar{
		display: block;
		width: 60px;
		height: 200px;
	}


###Function 
Sass supports actual functions as well, which are used inline and always require a return value

Pointless Example:

	@function weight($weight){
		@if $weight == bold{
			return 700;
		}
		@else{
			return 400;
		}
	}

	.foo{
		font-weight: weight(bold);
	} 

Output:

	.foo{
		font-weight: 700;
	}

Sass supports all the usual control flow stuff you'd expect from a proper programming language, as well as loops (for and each) and a number of variable types. There are a number of examples of these in the base folder's partials.