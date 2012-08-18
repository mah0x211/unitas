unitas
======

command line tool for compile javascript files.

    Usage:

        unitas [-h] -c /path/to/config [-o /path/to/output] [-g /path/to/closure_compiler]

        -h, --help : print usage(this document)

        -c, --config : path of configuration json file (required)

        -o, --output : path of output directory
        [default] current working directory

        -g, --gcc : path of google's closure compile command


    Config JSON format: 
        { 
            // use for compiled script file name and identifier name. 
            "name": "<script_name>", 

            // location path of source files 
            "srcs": [ 
                "</path/to/target/script.js>", 
                ... 
            ], 

            // parent object: default "window" 
            "parent": "<valid-identifier-name>", 

            // set object restriction if defined 
            "restriction": "<freeze|seal|preventExtensions>", 

            // gcc options: closure-compiler --help 
            "gcc": { 
                // default options 
                "warning_level": "VERBOSE", 
                "language_in": "ECMASCRIPT5_STRICT", 
                "summary_detail_level": 3, 
                "externs": "<output directory>/<name>_externs.js", 
                // fixed options 
                "js": "...", 
                "js_output_file": "..." 
            } 
        } 

    Preprocessor directives: 

        // MARK: @init:[<arg1>,<arg2>,...] 
        <arg>: argument of initializer. 

        // MARK: @src:begin 
        source code... 
        ... 
        // MARK: @src:end 
        slice source code from tail of @src:begin directive 
        to head of @src:end directive. 

        // MARK: @debug:begin 
        source code... 
        ... 
        // MARK: @debug:end 
        remove source code from head of @debug:begin directive 
        to tail of @debug:end directive. 

        // MARK: @extern:<extern-property>:<literal-notation> 
        <extern-property>: name of property 
        <literal-notation>: define type of property by literal notation. 

