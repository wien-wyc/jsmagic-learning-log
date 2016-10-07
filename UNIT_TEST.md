# 单元测试

[Mocha](http://mochajs.org/) 是一个 Node.js 的测试框架

[Chai](http://chaijs.com/) 是一个断言（assertion）框架

一般推荐行为驱动开发（BDD）的风格编写测试：

```javascript
describe('Array', function() {
  before(function() {
    // ...
  });

  describe('#indexOf()', function() {
    it('should return the index where the element first appears in the array', function() {
      [1,2,3].indexOf(3).should.equal(2);
    });
  });
});
```

可以使用 babel src -d lib -w 自动监听并转译，使用 mocha 'lib/\*\*/\*_test.js' -w 自动监听并测试（一般将 mocha 'lib/\*\*/\*\_test.js' 放到package.json的test脚本中就可以使用npm run test运行测试）。
