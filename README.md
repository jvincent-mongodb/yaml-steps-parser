# yaml-steps-parser
Convert YAML `steps` files to ReStructured Text `procedure` files. 

## Usage

Copy this script into the same directory as the YAML `steps` file you need to convert. 

Then run the following to generate a ReStructured Text `procedure` file that is equivilent to the existing YAML `steps` file:

```
python3 yaml_steps_to_rst.py <YAML steps filename>
```

The newly generated ReStructured Text file name will be the same as the YAML `steps` file, but it will have a `.rst` file extension. 
