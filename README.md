# meteorite-visualization


- Globe visual with globe.gl or whatever it's called
  - Configuration/styling for that

- Inculde and unpack meteorite data
  - Put into globe visual


## Method

PART 1: GLOBE SETUP
1. Open "Visual Studio Code" or another text editor. We are coding from scratch!
2. Create index.html
3. `Code <!DOCTYPE html>`, `<html>...</html>` with head and body tags
4. Add `<title>Meteor Visualization</title>` to the head tag
5. Include `<script src="//unpkg.com/globe.gl"></script>` in the head tag
6. Add `<div id="globe"></div>` to the body tag
7. Let's go back to the head. Add the following to the head tag:
   ```html
<style>
  body {
    margin: 0;
  }
</style>
    ```
1. 