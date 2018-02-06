# SASS breakpoint manager

*(5-10 minutes reading and understanding)*

*Your new SASS breakpoint mixin with **super powers!***
This is breakpoint solution based on Foundation 6 framework, simplified and made better.

```scss
// SETTINGS

// A list of named breakpoints. You can use these with the `breakpoint()` mixin to quickly create media queries.
// @type Map
$breakpoints: (
	small: 0,
	medium: 640px,
	large: 1024px,
	xlarge: 1200px,
	xxlarge: 1440px,
);

// The largest named breakpoint in which to include print as a media type - @media screen, print and (...)
$print-breakpoint: large;

// Import breakpoint manager mixin and supporting functions
@import 'breakpoint';

// YOUR STYLES

.test {
    color: #cacaca;
    
    /* medium only - (min-width: {{lower_bound_medium_breakpoint}}) and (max-width: {{upper_bound_medium_breakpoint}}) */
    @include breakpoint(medium only) {
        color: #bada55;
    }
    
    /* large up - (min-width: {{lower_bound_large_breakpoint}}) */
    @include breakpoint(large) {
        color: #000;
    }
}
```

In the file ***_breakpoint.scss*** is one mixin (breakpoint) with supporting functions.

## Mixin syntax

It's very easy!

```scss
.some-selector {
    @include breakpoint({{breakpoint}} {{direction}}) {
        /* css rules */
    }
}
```

**BREAKPOINT** *(string or number)* - can be key from $breakpoints map, or value (value can be in *em, rem,* or *px*. Unitless values are presumed like pixels). All inputs will be converted to '***em***' values.
   - **Examples:** *'small', 'medium', 'large', '400', '500px', '20em', '40rem'*.
   - **These inputs will throw console error**: *'0', 'null', '0 down' & empty string*. Also non-exist named (string) breakpoint will throw error. (You must defined all named breakpoints into *$breakpoint* map)
   - **Device oriented breakpoints**: *'portrait', 'landscape', 'retina'* 
   
**DIRECTION** *(string)* - is breakpoint direction. 
   - **Examples** - *'down', 'only', 'up'* (***up*** is default)
   - **Handler** - only **named** breakpoint (*small, medium,* etc.) can have *'only'* parameter. (because of the unit range).

# Instalation 
   **1.** Set up your $breakpoint map like in example above.
   **2.** Import ***_breakpoint.scss*** file via @import directive. (@import 'breakpoint.scss';)
   **3.** Do magic within selectors! *@include breakpoint(...) {}* !

# Examples

```scss
.test {
	padding: 10px;
	background-color: #c1c1c1;

	// medium only - (min-width: {{lower_bound_medium_breakpoint}}) and (max-width: {{upper_bound_medium_breakpoint}})
	@include breakpoint(medium only) {
		background-color: #bada55;
	}

	// medium and up - (min-width: {{lower_bound_medium_breakpoint}})
	@include breakpoint(medium) {
		//...
	}
	
	// large and down (small to large) - (max-width: {{upper_bound_large_breakpoint}})
	@include breakpoint(large down) {
		//...
	}

	// large and up - (min-width: {{lower_bound_large_breakpoint}})
	@include breakpoint(large) {
		//...
	}

	// Device oriented breakpoints
	// 
	// you can use "landscape","portrait" or "retina"

	// retina styles - (-webkit-min-device-pixel-ratio: 2), (min-resolution: 192dpi)
	@include breakpoint(retina) {
		//...
	}

	// landscape oriented devices - (orientation: landscape)
	@include breakpoint(landscape) {
		//...;
	}

	// landscape oriented devices - (orientation: portrait)
	@include breakpoint(portrait) {
		//...
	}

	// Custom breakpoints
	//
	// have the same logic
	// @include breakpoint({{value}} {{direction}})
	// value     - is automaticly converted to 'em' - from rem, px, even without value
	// direction - down, only or up (default one - you don't need to write it)


	// custom breakpoint - (min-width: {{em_value}}) 
	@include breakpoint(600px) {
		//...
	}

	// custom unitless breakpoint (it's assumed that it's px) - (max-width: 31.25em) 
	@include breakpoint(500 down) {
		//...
	}

	// custom breakpoint - (min-width: 25em) 
	@include breakpoint(25rem) {
		//...
	}


	// Handling errors
	// 0 + anything will add styles without wrapping to @media

	@include breakpoint(0 down) {
		//... error
	}

	@include breakpoint(0 up) {
		// this is actualy ok and will pass!!
	}

	@include breakpoint(0) {
		//...
	}
}
```

Enjoy! 
