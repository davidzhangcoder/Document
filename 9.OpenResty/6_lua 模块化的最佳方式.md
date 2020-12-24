6.lua 模块化的最佳方式  
20201115

```
http://www.dahouduan.com/2017/12/07/lua-module-best-practice/

1.
用“方式二:在包中定义类”，似乎是需要用到对象中的属性，如下面例子中的self.width和self.height

2.
方式一 通过返回表来实现
local M = {}

function M.play()
    print("开始");
end

function M.quit()
    print("退出")
end

return M;

调用：
local game = require('game')
game.play()   
方式二 在包中定义类
local _M = {}

_M._VERSION = '1.0'

local mt = { __index = _M }

function _M.new(self, width, height )
    return setmetatable({width = width, height = height}, mt)
end

function _M.get_square( self )
    return self.width * self.height
end

return _M

调用：
local square = require('square')
local s1 = square:new(2, 3)
print(s1:get_square())
```