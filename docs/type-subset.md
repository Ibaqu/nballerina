Grammar for type definitions currently supported for semantic type checking.

Unlike the grammar in the Ballerina language spec, this make precedence explicit.

Undefined symbols as defined in the currently implemented subset.

```
type-defn := "type" identifier type-desc ";"

type-desc := function-td 

function-td =
    union-td
    | "function" identifier "(" type-desc-list ")" ["returns" function-td]

union-td :=
    intersection-td
    | union-td "|" intersection-td

intersection-td :=
    postfix-td
    | intersection-td "&" postfix-td

postfix-td := 
  primary-td
  | postfix-td "[" "]"
  | postfix-td "?"

primary-td :=
  predefined-td
  | int-td
  | map-td
  | record-td
  | tuple-td
  | error-td
  | function-td
  | nil-td
  | singleton-td
  | td-ref 
  | "(" type-desc ")"
    
nil-td := "(" ")"
int-td := "int" [ ":" identifier ]
map-td := "map" "<" type-desc ">"
error-td := "error" ["<" type-desc ">"]
// XXX handle "..."
tuple-td := "[" type-desc-list "]"
td-ref := identifier // can also refer to const definition

predefined-td :=
    "boolean"
    | "decimal"
    | "float"
    | "string"
    | "xml"
    | "typedesc"
    | "handle"
    | "any"
    | "never"
    | "json"
    | "byte"
    | "readonly"
    | "true"
    | "false"

singleton-td = simple-const-expr
```