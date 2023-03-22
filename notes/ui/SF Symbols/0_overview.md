# OVERVIEW

Iconography lib designed to integrate with San Francisco, Apple platform system font.

Come in 9 weights and 3 scales, and automatically align with text labels. Can be exported and edited using vector graphics editing tools to create custom symbols with shared design characteristics and a11y features.

## Download

Tool to view symbols:

[https://developer.apple.com/sf-symbols/](https://developer.apple.com/sf-symbols/)

## Usage in Code

1. Find symbol name using tool:
    ![SYmbol](/assets/sf_symbol.png)

2. Use `Image` to display symbol:

    ```swift
    Image(systemName: "plus.circle")
    ```
