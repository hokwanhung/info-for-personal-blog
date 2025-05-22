# Tailwind to Quasar Migration Guide

This guide helps you convert Tailwind CSS classes to their Quasar equivalents.

## Spacing

### Padding

| Tailwind | Quasar    | Description                            |
| -------- | --------- | -------------------------------------- |
| p-0      | q-pa-none | No padding                             |
| p-1      | q-pa-xs   | Extra small padding on all sides       |
| p-2      | q-pa-sm   | Small padding on all sides             |
| p-4      | q-pa-md   | Medium padding on all sides            |
| p-6      | q-pa-lg   | Large padding on all sides             |
| p-8      | q-pa-xl   | Extra large padding on all sides       |
| px-4     | q-px-md   | Medium padding on left and right sides |
| py-2     | q-py-sm   | Small padding on top and bottom sides  |
| pt-4     | q-pt-md   | Medium padding on top side             |
| pr-4     | q-pr-md   | Medium padding on right side           |
| pb-4     | q-pb-md   | Medium padding on bottom side          |
| pl-4     | q-pl-md   | Medium padding on left side            |

### Margin

| Tailwind | Quasar    | Description                               |
| -------- | --------- | ----------------------------------------- |
| m-0      | q-ma-none | No margin                                 |
| m-1      | q-ma-xs   | Extra small margin on all sides           |
| m-2      | q-ma-sm   | Small margin on all sides                 |
| m-4      | q-ma-md   | Medium margin on all sides                |
| m-6      | q-ma-lg   | Large margin on all sides                 |
| m-8      | q-ma-xl   | Extra large margin on all sides           |
| mx-4     | q-mx-md   | Medium margin on left and right sides     |
| my-2     | q-my-sm   | Small margin on top and bottom sides      |
| mt-4     | q-mt-md   | Medium margin on top side                 |
| mr-4     | q-mr-md   | Medium margin on right side               |
| mb-4     | q-mb-md   | Medium margin on bottom side              |
| ml-4     | q-ml-md   | Medium margin on left side                |
| mx-auto  | q-mx-auto | Auto margin on left and right (centering) |

## Flexbox & Grid

| Tailwind        | Quasar          | Description                        |
| --------------- | --------------- | ---------------------------------- |
| flex            | row             | Display flex with row direction    |
| flex-col        | column          | Display flex with column direction |
| items-center    | items-center    | Align items center                 |
| items-start     | items-start     | Align items to start               |
| items-end       | items-end       | Align items to end                 |
| justify-center  | justify-center  | Justify content center             |
| justify-between | justify-between | Justify content space-between      |
| justify-around  | justify-around  | Justify content space-around       |
| justify-start   | justify-start   | Justify content flex-start         |
| justify-end     | justify-end     | Justify content flex-end           |
| flex-wrap       | wrap            | Flex items wrap                    |
| flex-nowrap     | no-wrap         | Flex items don't wrap              |
| flex-1          | col             | Flex grow 1                        |
| gap-4           | q-gutter-md     | Medium gap between items           |

## Sizing

| Tailwind | Quasar        | Description      |
| -------- | ------------- | ---------------- |
| w-full   | full-width    | Width 100%       |
| h-full   | full-height   | Height 100%      |
| h-screen | window-height | Height 100vh     |
| w-screen | window-width  | Width 100vw      |
| max-w-md | (custom)      | Custom max width |

## Typography

| Tailwind      | Quasar                    | Description          |
| ------------- | ------------------------- | -------------------- |
| text-xs       | text-caption              | Extra small text     |
| text-sm       | text-body2                | Small text           |
| text-base     | text-body1                | Base size text       |
| text-lg       | text-subtitle2            | Large text           |
| text-xl       | text-subtitle1            | Extra large text     |
| text-2xl      | text-h6                   | 2xl text (heading 6) |
| text-3xl      | text-h5                   | 3xl text (heading 5) |
| text-4xl      | text-h4                   | 4xl text (heading 4) |
| text-5xl      | text-h3                   | 5xl text (heading 3) |
| text-6xl      | text-h2                   | 6xl text (heading 2) |
| text-7xl      | text-h1                   | 7xl text (heading 1) |
| font-bold     | text-weight-bold          | Bold font weight     |
| font-semibold | text-weight-medium        | Medium font weight   |
| font-normal   | text-weight-regular       | Regular font weight  |
| font-light    | text-weight-light         | Light font weight    |
| italic        | italic                    | Italic text          |
| underline     | text-decoration-underline | Underlined text      |
| text-center   | text-center               | Center-aligned text  |
| text-left     | text-left                 | Left-aligned text    |
| text-right    | text-right                | Right-aligned text   |
| text-justify  | text-justify              | Justified text       |

## Colors

Quasar uses its own color system, with classes like:

| Quasar         | Description                   |
| -------------- | ----------------------------- |
| text-primary   | Primary color text            |
| text-secondary | Secondary color text          |
| text-accent    | Accent color text             |
| text-positive  | Positive (success) color text |
| text-negative  | Negative (error) color text   |
| text-warning   | Warning color text            |
| text-info      | Info color text               |
| bg-primary     | Primary color background      |
| bg-secondary   | Secondary color background    |

## Display & Visibility

| Tailwind     | Quasar       | Description                          |
| ------------ | ------------ | ------------------------------------ |
| hidden       | hidden       | Display none                         |
| block        | block        | Display block                        |
| inline       | inline       | Display inline                       |
| inline-block | inline-block | Display inline-block                 |
| invisible    | invisible    | Visibility hidden                    |
| sm:hidden    | lt-sm-hide   | Hidden on screens smaller than small |
| md:block     | gt-sm        | Visible on screens medium and larger |

## Positioning

| Tailwind | Quasar            | Description                                    |
| -------- | ----------------- | ---------------------------------------------- |
| relative | relative-position | Position relative                              |
| absolute | absolute          | Position absolute                              |
| fixed    | fixed             | Position fixed                                 |
| sticky   | sticky            | Position sticky                                |
| top-0    | (combined)        | Top 0 - use fixed-top or absolute-top          |
| right-0  | (combined)        | Right 0 - use fixed-right or absolute-right    |
| bottom-0 | (combined)        | Bottom 0 - use fixed-bottom or absolute-bottom |
| left-0   | (combined)        | Left 0 - use fixed-left or absolute-left       |
| inset-0  | (combined)        | All sides 0 - use fixed-full or absolute-full  |

## Other Utilities

| Tailwind        | Quasar          | Description          |
| --------------- | --------------- | -------------------- |
| shadow          | shadow-1        | Small shadow         |
| shadow-md       | shadow-2        | Medium shadow        |
| shadow-lg       | shadow-4        | Large shadow         |
| shadow-xl       | shadow-8        | Extra large shadow   |
| rounded         | rounded-borders | Rounded borders      |
| rounded-full    | rounded-borders | Full rounded borders |
| cursor-pointer  | cursor-pointer  | Pointer cursor       |
| overflow-hidden | overflow-hidden | Overflow hidden      |
| overflow-auto   | overflow-auto   | Overflow auto        |
| z-50            | z-top           | High z-index         |
| z-max           | z-max           | Maximum z-index      |