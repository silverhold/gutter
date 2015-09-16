# Gutter Helper
Gutter helper is a scss tool designer to quickly generate helpers classes for margin and padding.

## Get started
Gutter helper is available via bower with the following command
```
  bower install gutter-helper
```
## Concept
Gutter Helper is based on one single value (the `$gutter-helper--gutter variable` located into the `_parameters.scss` file) declinated through multipliers, properties (`margin` and `padding`), directions and responsive breakpoints and compiled as css classes.

## Usage
### Generate the code
The idea behind Gutter Helper is to fit perfectly to your needs and not generate too much useless css classes. For it you have a bunch of scss variables to set :

#### `$gutter-helper--gutter`
As mentioned previously, this is the base value for all the helper classes generated
##### Default
```
$gutter-helper--gutter: 30px !default;
```

#### `$gutter-helper--multipliers`
A scss list that will regroup all the coefficient used to be multiplied to `$gutter-helper--gutter`, the scss will loop through this list to generate multiplied helpers. Multplier can not be more than 9.9, only one digit behind the decimal point.
##### Default
```
$gutter-helper--multipliers: (.5, 1, 2) !default;
```

#### `$gutter-helper--properties`
A scss list that will regroup the kind of property that could be generated. The list can only contain 'margin' and/or 'padding'
##### Default
```
$gutter-helper--properties: ('margin', 'padding') !default;
```

#### `$gutter-helper--directions`
A scss list that will regroup all the direction that can be generated. For example 'top' will generate class for the specific top direction will property as `margin-top` or `padding-top`. The only accepted value in this list are:
* `'a'`: for all, will generate for example `margin` or `padding` property (without specific direction)
* `'x'`: shortcut for `left` & `right`
* `'y'`: shortcut for `top` & `bottom`
* `'top'`, `'right'`, `'bottom'` and/or `'left'`
##### Default
```
$gutter-helper--directions: ('a', 'x', 'y' 'top', 'right', 'bottom', 'left') !default;
```

#### `$gutter-helper--breakpoints`
A scss list that will regroup all the breakpoint and the value of the media queries for the responsive classes generated. The key is a string used into the class name as breakpoint name, the value a media querie value for `@media (min-width: {your value})` statement (mobile first philosophy)
##### Default
```
$gutter-helper--breakpoints: ('xs': 0, 'sm': 768px, 'md': 992px, 'lg': 1200px) !default;
```

### Use the code
Once you have set your variable, you are ready to go and use your classes ! You have follow the pattern below:

```html
<div class="gutter-{property}-{direction}-{multiplier}x-{breakpoint}"></div>
```

Some observation :
* In order to have not to heavy class names, `padding` and `margin` have respective `p` and `m` aliases instead. `gutter-padding-...` will not work
* For all direction, use `a` like `gutter-p-a-xs`
* For `left` and `right` direction, use `x` like `gutter-p-x-2x-xs`
* For `top` and `bottom` direction, use `y` like `gutter-p-y-2x-xs`
* If you want to use an helper class with 1 as multiplier just don't put any mutliplier in your class name like `gutter-p-a`
* If you want to use a decimal multiplier, remove the decimal point like `gutter-p-a-15x-xs`
* If your decimal multiplier is less than 0, put a 0 in your class. For example a .5 mutlplier class must be `gutter-p-a-05x-xs`
* You can not write any breakpoint descriminator in your helper class for avoid media queries like `gutter-p-a-15x`.
