# 2xz

> (Re)compresses everything to .xz or .tar.xz.

## Why do that?
Because .xz compresses fairly better than .zip or .gz. I've seen one file.tar.gz of mine shrink from 32Mb to 8Mb when converted to .tar.xz — and that is especially because of the smart way xz handles compressing when many of the files are repeated or very similar in contents. 

For more, check `xz` in [Wikipedia](https://en.wikipedia.org/wiki/Xz), or the [developer's page](http://tukaani.org/xz/).

Below: supported extensions to convert. Other files will be xz'd. Dirs will be tar.xz'd.
```bash
.7z .ar .bz2 .cb7 .cbr .cbt .cbz .gz .jar .lz .lzma .lzo .rar .tar .tar.bz2 
.tar.7z .tar.gz .tar.lz .tar.lzma .tar.lzo .tbz .tbz2 .tgz .tlz .tzo .Z .zip 
.xz* .tar.xz* .txz*
```
(* yep, we recompress them, to ensure maximum compression)

## Usage and examples
```bash
2xz                       # Help menu

2xz [-n] <files>
2xz f1.jar f2.zip f3.tgz  # Converts those three, and backs up originals at ./OldArchives
2xz -n *.tar.gz           # Converts all .tar.gz and deletes the originals.
```

## Dependencies
Must have installed `unrar-free`, `lzip`, `lzop`, `p7zip-full`, `gzip`, `bzip2`
if you want to extract, respectively: `.rar`, `.lzip`, `.lzop`, `.lzma`, `.7z`, `.gz`, `.bz2`.
Try:
`sudo apt-get install xz-utils unrar-free lzip lzop p7zip-full gzip bzip2`


## Limitations (not exhaustive)
* Recognizes filetype by extension, not by `/usr/share/file/magic`.
* Does not handle password protection.
* Limit cases not thoroughly tested. (Filenames with crazy characters, nested archives etc.)
* Conversion of filenames with spaces not thoroughly tested; be cautious. I recommend `detoxing` those files. (`sudo apt-get install detox`)

## Final notes
1. To extract a `.xz`, run: `unxz MYFILE.xz`. To extract a `.tar.xz`, run: `tar xvJf MYFILE.tar.xz`.
2. Note that `unrar-free` fails often. If you have only a few `.rar`, I'd suggest extracting them by hand with something like `Peazip`, and then recompressing the files normally to `.tar.xz`.
3. **USE IT AT YOUR OWN RISK**. I wrote this carefully — but I suggest you back up your input files before using `2xz`, as I may have overlooked something critical. Don't blame me if you run `2xz` and your archive gets warped or your cat microwaved. But tell me about it, or fix it, so we can avoid other people's cat from being microwaved.

