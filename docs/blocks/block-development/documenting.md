# Documenting your block

There is a standard way to document a nio Block. Much of this documentation can be generated automatically using the `nio-cli`.

> **[info] Note**
>
> These instructions assume that you are working in a nio project directory or that your block directory is inside of a directory labeled `blocks`. In other words, "the root of your project" is equivalent to the directory where you can access your block repo with the path `blocks/<your block repo>`.
>

1. Create a `release.json` file. Once you have built your block, navigate to the root of your project directory (or, if you aren't developing your block in a project directory, to the directory below `blocks/<block repo name>`) and type

  ```
  nio buildrelease <block repo name>
  ```

  This will create a `release.json` file with meta information about your block.

2. Create a `spec.json` file. To create your `spec.json` file, type

  ```
  nio buildspec <block repo name>
  ```

  Navigate into your `spec.json` file and manually add a text string description to any key labeled "description". You will need to add a description to the block and its properties, commands, inputs, and outputs.

  ```py
  "description": "List of attribute names and corresponding values to add to the incoming signals."
  ```

3. Generate your `README.md` file. Once your `spec.json` is complete, you are ready to build your block's README. Navigate into the block folder and type

  ```
  nio buildreadme
  ```

  This will populate the README. Manually add any dependencies in this format

  ```
  Dependencies
  ------------
  - face_recognition
  - numpy
  - opencv-python
  ```

  You can also add example code and other helpful information at the bottom.

4. Finally, check your block. To check your block, remain in your block directory and run

  ```
  nio blockcheck
  ```

  to check and lint your block. It will check PEP8 styles, confirm you have added descriptions to your `spec.json`, and check your `README.md`, `release.json`, and class and file names.
