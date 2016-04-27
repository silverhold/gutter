# Gutter Helper
Gutter helper is a scss tool designer to quickly generate helpers classes for margin and padding.

## Get started
Gutter helper is available via bower with the following command
```
bower install trowel-gutter
```
## Concept
Gutter Helper is based on one single value (the `$gh-gutter variable` located into the `_parameters.scss` file) declinated through multipliers, properties (`margin` and `padding`), directions and responsive breakpoints and compiled as css classes.

## Usage
### Generate the code
The idea behind Gutter Helper is to fit perfectly to your needs and not generate too much useless css classes. For it you have a bunch of scss variables to set :

#### `$gh-gutter`
As mentioned previously, this is the base value for all the helper classes generated.
##### Default
```
$gh-gutter: 30px !default;
```

#### `$gh-multipliers`
A scss list that will regroup all the coefficient used to be multiplied to `$gh-gutter`, the scss will loop through this list to generate multiplied helpers. Multplier can not be more than 9.9, only one digit behind the decimal point.
##### Default
```
$gh-multipliers: (.5, 1, 2) !default;
```

#### `$gh-properties`
A scss list that will regroup the kind of property that could be generated. The list can only contain 'margin' and/or 'padding'. If you are using `px` units, the decimal for multiplied number will be rounded.
##### Default
```
$gh-properties: ('margin', 'padding') !default;
```

#### `$gh-directions`
A scss list that will regroup all the direction that can be generated. For example 'top' will generate class for the specific top direction will property as `margin-top` or `padding-top`. The only accepted value in this list are:
* `'a'`: for all, will generate for example `margin` or `padding` property (without specific direction)
* `'x'`: shortcut for `left` & `right`
* `'y'`: shortcut for `top` & `bottom`
* `'top'`, `'right'`, `'bottom'` and/or `'left'`
##### Default
```
$gh-directions: ('a', 'x', 'y', 'top', 'right', 'bottom', 'left') !default;
```

#### `$gh-responsive`
A scss boolean that will generate (if true), responsive helper class based on the [responsive-helper breakpoints](https://github.com/LoicGoyet/responsive-helper).
##### Default
```
$gh-responsive: true !default;
```

#### Deprecated variables
All the listed variables below are deprecated and replaced by its equivalent referenced. Don't panic, this is just some naming convention fixes, so there is no changes excepted the name of the variable, no feature change.

* `$gutter-helper--gutter` is deprecated and replaced by the `$gh-gutter`
* `$gutter-helper--multipliers` is deprecated and replaced by the `$gh-multipliers`
* `$gutter-helper--properties` is deprecated and replaced by the `$gh-properties`
* `$gutter-helper--directions` is deprecated and replaced by the `$gh-directions`
* `$gutter-helper-responsive` is deprecated and replaced by the `$gh-responsive`


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


## The `get-gutter()` function
You can use the `get-gutter()` function that will return a value for depending of the parameter will pass (default value is `1`). This parameter must be a number that is indexed into the the `$gh-multipliers` map.

```scss
$gh-gutter: 30px;
$gh-multipliers: (.5, 1, 2);

html {
    padding-top: get-gutter(2);
}

// Will compile
html {
    padding-top: 60px;
}
```

## Using Gutter Helper with performance
Gutter Helper can generates a lot of css, and it could be very costly on a performance perspective. In order to fully enjoy gutter helper without any generated classes unused we recommand the usage of [unscss](https://github.com/giakki/uncss)
