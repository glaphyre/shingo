<h1 align="center">shingo</h1>
<div align="center">
    <a href="https://pesde.dev/packages/glaphyre/shingo">
        <img alt="pesde" src="" />
    </a>
</div>

<div align="center">
    another signal implementation
</div>

<div>&nbsp;</div>

`shingo` is *sigh* yet another signal implementation written in luau which uses doubly linked-lists to connect callback functions. It is a typechecked module, provides documentation via `luau-lsp`, and uses `snake_case`.

## Installation

#### via pesde

```sh
# add shingo
pesde add glaphyre/shingo

# install all packages
pesde install
```

### from github
- clone the repo
- copy the src/shingo.luau file
- paste it into your project

## Crash Course
```luau
local shingo = require("./path/to/shingo")

-------------------------------------------------

--// void signal (no parameters)
local signal1: shingo.Signal = shingo.new()

--// single parameter signal
local signal2: shingo.Signal<number> = shingo.new()

--// multi parameter signal
local signal3: shingo.Signal<number, string, bool> = shingo.new()

-------------------------------------------------

local connection = signal1:connect(print) --// typechecked!

-------------------------------------------------

signal1:once(function(n: number) --// typechecked!
    print(`i will only run once!`)
end)

-------------------------------------------------

signal1:fire(100) --// prints i will only run once! and 100
signal1:fire(100) --// prints 100

-------------------------------------------------

connection:disconnect() --// disconnects the function, preventing the callback from running the next signal fire

-------------------------------------------------

local n = signal1:wait() --// yields the code until the next signal fire
print(`i waited for {n}!`)

-------------------------------------------------

signal1:destroy() --// disconnects all connections and makes it unusable
signal1:fire() --// error: signal is destroyed

-------------------------------------------------
```

