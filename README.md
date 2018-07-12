# BEM style guide

- [BEM](#1)
  - [General Idea](#1.1)
  - [BEM Principles](#1.2)
  - [Rules to Follow](#1.3)
  - [File Structure](#1.4)

<a id="1.1"></a>
### General idea:

BEM is a naming convention which does a good job to help to provide a maintainable architecture with a recognizable terminology.
BEM stands for “Block”, “Element”, “Modifier”.

B__E--M

<a id="1.2"></a>
### BEM Principles:

#### 1. What is block?

Block is a top-level abstraction, it's a logically and functionally independent page component which easy to re-use. It's an entity, a “building block” of an application. To implement a block, we write CSS that describes appearance of the block, not its position.

#### 2. What is element?
Element is a part of a block that can't be used outside.

#### 3. What is modifier?
Modifier is a BEM entity that defines the appearance and behavior of a block or an element.

<a id="1.3"></a>
### Rules to follow:

- CSS for every block should be located in separate files so it's easy to find them by <kbd>CMD</kbd>+<kbd>P</kbd>
- Blocks don't have position/margin styles so they are reusable.

How to position elements:

```
<div class=“block1”>
    <div class=“block1__element block2”></div>
</div>
```

`.block1__element` class is responsible for the position of block2.

- `block__element__element` - this structure can never exist.

```
<div class=“block”>
    <div class=“block__element1">
        <div class=“block__element2”></div>
    </div>
</div>
```

In sass/stylus:

```
.block {
    $this: &

    &__element1 {
        @at-root {
            #{$this}__element2 & {

            }
        }
    }
}
```

- `.block > div` or `.block1 .block2` - this structures can never exist, nested selectors are not allowed as it will screw up the flatness.
- By adding prefixes to entities names we can avoid conflicts with external libraries:
    - c- for component
    - g- for grid
    - js- for javascript hooks

- Global modifiers naming convention: `._global-modifier`. Try to avoid creating global modifiers. In most cases it’s better to create a block modifier instead of using global modifiers.


<a id="1.4"></a>
### File Structure:

4. The structure of the files can be the following:

```
styles/
    components/
        Reusable components are located here
    grid/
        Grid if needed (we use bootstrap so probably not)
    utils/
        Functions/Variables/Mixings/Placeholders
        libs.styl to combine all the utils together for convinient export

style.styl
```

It's a good practice to group block CSS files in folders under the `components` folder. 
For example:

```
styles/
    components/
        form/
            c-btn.styl
            c-select.styl
            c-input.styl
```