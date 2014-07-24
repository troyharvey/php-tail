#Tail

It's simply a library for polling text files for changes. Like good old tail. Theres no inotify support though, but it will take a roundtrip and look for changes to the file size each .5 sec. So if that is quick enough for you, this is a really simple solution.


##How to use

Initial part:

```php
$tail = new \Desipa\Tail(__DIR__ . '/save.json');
$tail
    ->addFile('file1.txt')
    ->addFile('file2.txt')
    ->addFile('file3.txt')
;
```

Example on how to tail for each line:

```php
$tail->listenForLines(function($filename, $line) {
    print "$filename - $line\n";
});
```

Example on how to tail for each update:

```php
$tail->listen(function($filename, $chunk) {

    foreach (explode("\n", $chunk) as $text) {
        $text = trim($text);
        if (empty($text)) {
            continue;
        }

        print "$filename - $text\n";
    }

});
```

##TODO:
* Write comments and doc-blocks for the code.
* Write unit-tests.
* Make the wait-time a variable.
