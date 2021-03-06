# Textual Comparison table Generator (tcg)

Personal mini utility to make comparison tables, written in Java.

This is suitable for users who write notes on pure text and want to compare things.

It can convert a markdown like doc to a text table which can then be copied to anywhere.

Since it use markdown, you can enjoy zero cost syntax highlighting.

```text
    # Input/Output
    ```SML
    fun copyFile(name1, name2) =
        let
            val file1 = TextIO.openIn name1
            val s     = TextIO.inputAll file1
            val _     = TextIO.closeIn file1
            val file2 = TextIO.openOut name2
        in
            TextIO.output(file2, s);
            TextIO.closeOut file2
    end
    ```
    ```Ocaml
    let copy_file name1 name2 =
       let file1 = open_in name1 in
       let size = in_channel_length file1 in
       let buf = String.create size in
           really_input file1 buf 0 size;
           close_in file1;
       let file2 = open_out name2 in
           output_string file2 buf;
           close_out file2
    ```
    # Local Declarations
    ```SML
    fun pyt(x,y) =
       let
          val xx = x * x
          val yy = y * y
       in
          Math.sqrt(xx + yy)
       end
    ```
    ```Ocaml
    let pyt x y =
       let xx = x *. x in
       let yy = y *. y in
       sqrt (xx +. yy)
    ```
```

will be converted to

```text
Input/Output
-SML---------------------------------------+-Ocaml------------------------------------
 fun copyFile(name1, name2) =              | let copy_file name1 name2 =               
     let                                   |    let file1 = open_in name1 in           
         val file1 = TextIO.openIn name1   |    let size = in_channel_length file1 in  
         val s     = TextIO.inputAll file1 |    let buf = String.create size in        
         val _     = TextIO.closeIn file1  |        really_input file1 buf 0 size;     
         val file2 = TextIO.openOut name2  |        close_in file1;                    
     in                                    |    let file2 = open_out name2 in          
         TextIO.output(file2, s);          |        output_string file2 buf;           
         TextIO.closeOut file2             |        close_out file2                    
======================================================================================

Local Declarations
-SML---------------------------------------+-Ocaml------------------------------------
 fun pyt(x,y) =                            | let pyt x y =                             
    let                                    |    let xx = x *. x in                     
       val xx = x * x                      |    let yy = y *. y in                     
       val yy = y * y                      |    sqrt (xx +. yy)                        
    in                                     |                                           
       Math.sqrt(xx + yy)                  |                                           
======================================================================================
```

## Usage

1. Install newest Java.
2. Grab `tcg.run` or `tcg.jar` from Github releases
3. `./tcg.run <filename>.md` or  `java -jar tcg.jar <filename>.md`

### Config

There are no command line flags, YAML front matters do all the config.

```yaml
---
tabsize: 4
ending: true/false
---
```

## Build

+ `make` -> single executable `tcg.run`,
+ `make tcg.jar`
+ `make test`


## Misc

+ Only tested on JDK 16.
+ Not optimal Java, as I never code much java before.

## License

GPL-3.0-only