# nr-orb-demo

This project demonstrates how you can instrument your CircleCI Builds with build annotations, and capture incremental build data for transmission to New Relic.

## Orb Development
You can find the code repository for the orb at [jhawkinsfuturehack/nr-futurehack-orb](https://github.com/jhawkinsfuturehack/nr-futurehack-orb)

![Example Dashboard](https://github.com/jhawkinsfuturehack/nr-orb-demo/blob/main/images/Test_Build_Dashboard___New_Relic_One.png)

## Setup
To setup the project, you need to add your `NR_LICENSE_KEY` to your circleCI project:
 -> **Project Settings**->**Environment Variables**->**Add Environment Variable**


![Configuration](https://github.com/jhawkinsfuturehack/nr-orb-demo/blob/main/images/Environment_Variables_-_nr-orb-demo.png?raw=true)

## Usage

To instrument your build, you first need to include the orb for the `nr-futurehacak/annotate` orb [code](https://github.com/jhawkinsfuturehack/nr-futurehack-orb)
```
orbs: 
  annotate: nr-futurehack/annotate@dev:802c07bd0e6eb0add0b6368453666349635d8f8b
```

Once you've added the orb, you can make use of the **annotate** to annotation:
```
    - annotate/step:
        trace_id: "Checkout"
```

At the end of your script, you must add an `annotate/send` command in order to transmit to New Relic.
```
     - annotate/send
```

## Example
```
      - annotate/step:
          trace_id: "Checkout"
      - checkout
      
      - annotate/step:
          trace_id: "Code Compilation"
      - run:
          name: "Compile"
          command: |
            echo "<Your Build Command>"
 
      - annotate/step:
          trace_id: "Running Tests"
      - run:
          name: "Compile"
          command: |
            echo "<Your Build Command>"
     
      - annotate/send
```
