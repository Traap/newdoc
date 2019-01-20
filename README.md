## newdoc - Seed a LaTeX document with standard content. 
The **newdoc** repository simplifies initializing LaTeX documnets the meet
minimum requirements defined by **autodoc, **docbld**, and **tlc-article**. 

# Prerequisites 
1. [autodoc](https://GitHub.com/Traap/autodoc.git)
1. [docbld](https://GitHub.com/Traap/docbld.git)
1. [MiKTeX](https://miktex.org/download)
1. [tlc-article](https://GitHub.com/Traap/tlc-article.git)


### Installation
```bash
$ cd $HOME
$ git clone git@github.com:Traap/newdoc.git
```

### Add this function to .bashrc
```bash
NEWDOCPATH=${HOME}/git/newdoc

export NEWDOCPATH

function newdoc() {
  ${newdocPATH}/newdoc 
}
```

### Use
Run newdoc to create the scaffolding for a new LaTeX document that is compatible
with autodoc, docbld, and tlc-article.
```
Usage: newdoc [OPTIONS]

OPTIONS
  --dir=path/to/dir              Directory to create.
  --file=fileName                File to create.
  --title='Your Document Title'  Document title to use.

  --logo                         Seed document a logo.
  --share                        Use shared header and footer data.

  --help                         Display this help message.

```
### Example
```
newdoc --dir report/summary --file=001 --title='Foo' --shared --logo
newdoc --dir report/summary --file=002 --title='Bar' --shared
newdoc --dir report/summary --file=003 --title='Baz' 
```
### Copied Files
| Option   | Files                        | Destination
| ---      | ---                          | ---         
| --file   | fileName.tex fileName.texx   | path/to/dir/filename path/to/dir/filename/data
| --logo   | logo.png                     | path/to/dir/filename/data
| --shared | additional-layout-shared.tex | path/to/dir/shared/data/additional-layout.tex

## Project Management
Please refer to my [Lightweight Project Mangement](https://github.com/Traap/lpm)
for the project management strategy I use.
