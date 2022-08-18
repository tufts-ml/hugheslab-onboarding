What's an easy way to make sure no file in your codebase contains strings of text you don't want to appear?

Use command line tools in Unix!

From your root directory of your project, use this:

```
$ find . -type f | xargs grep -i {KEYWORD}
```

Remember that the -i switch for grep means "ignore case", so it 'll match TUFTS or Tufts or tufts

# does any file contain TUFTS?

```
$ find . -type f | xargs grep -i tufts
./README.txt: This program was made at Tufts University   
```

# REPLACE ALL 'TUFTS' with blank

```
$ find . -name 'README.txt' | xargs perl -pi -e 's/Tufts//g'
```

# Verify it worked

```
$ find . -type f | xargs grep -i tufts

```

Here, a blank response means no files match
