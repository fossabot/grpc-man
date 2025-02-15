# grpc-man

> A client to call gRPC server methods on the fly. 一个 gRPC 客户端，可以灵活地调用 gRPC 服务。

> 名字灵感来源于 `post-man`。


[![996.icu](https://img.shields.io/badge/link-996.icu-red.svg)](https://996.icu)
[![LICENSE](https://img.shields.io/badge/license-Anti%20996-blue.svg)](https://github.com/996icu/996.ICU/blob/master/LICENSE)
[![Build Status](https://travis-ci.com/Jeff-Tian/grpc-man.svg?branch=master)](https://travis-ci.com/Jeff-Tian/grpc-man)
[![NPM version](https://badge.fury.io/js/grpc-man.png)](http://badge.fury.io/js/grpc-man)
[![npm download][download-image]][download-url]
[![Dependencies Status](https://david-dm.org/Jeff-Tian/grpc-man.png)](https://david-dm.org/jeff-tian/grpc-man)
[![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg)](https://github.com/semantic-release/semantic-release)
[![Git commit with emojis!](https://img.shields.io/badge/gitmoji-git%20commit%20with%20emojis!-brightgreen.svg)](https://gitmoji.js.org)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2FJeff-Tian%2Fgrpc-man.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2FJeff-Tian%2Fgrpc-man?ref=badge_shield)

[![Quality gate](https://sonarcloud.io/api/project_badges/quality_gate?project=Jeff-Tian_grpc-man)](https://sonarcloud.io/dashboard?id=Jeff-Tian_grpc-man)

[download-image]: https://img.shields.io/npm/dm/grpc-man.svg?style=flat-square
[download-url]: https://npmjs.org/package/grpc-man

# 有什么用？

本包提供了一个轻量级的 gRPC 客户端实现，可以用来快速验证你的 gRPC 服务是否正确工作。

当然，它只提供了连接 gRPC 服务的方法，具体运行结果需要自行写代码验证。

作者在实际项目中使用 `Mocha` 测试框架，也非常推荐你使用它。后面会有在 `Mocha` 框架中使用此包的示例代码。

当然，你也可以在别的测试框架中使用本包，比如本项目自身使用了 `jest`（`jest` 很优秀，但实际使用下来，我感觉不如 `Mocha` 快）。

# 安装:

```bash
# 如果你想全局运行:
npm install -g grpc-man

# 如果你想在项目的测试代码里使用它:
npm install --save-dev grpc-man
```

# 用在 `javascript` 项目里：

```javascript
import GrpcClient from 'grpc-man/lib/Client';

async function main() {
  const client = new GrpcClient('<yourhost>:<your port>', __dirname + 'your.proto');

  await client.grpc.youpackage.YourService.yourMethod(arg);
}
```

# 用在测试里:

如果你的项目使用 gRPC 为客户提供服务，那么在你的项目的自动化测试中，你可以用它来帮助调用你的 gRPC 服务:

### mocha 示例

示例用到的 proto 文件[在这里](./src/__tests__/proto/helloworld.proto)。

```typescript
import assert = require('assert');
import GrpcClient from 'grpc-man/lib/Client';

describe('grpc', () => {
  it('可以打招呼', async () => {
    const client = new Client('0.0.0.0:8899', __dirname + '/./proto/helloworld.proto');

    const res = await client.grpc.helloworld.Greeter.sayHello({ name: 'name' });
    assert.deepEqual(res, { message: 'Hello name' });
  });
});
```

如果你采用 `jest` 测试框架，那么可以参考[本包的测试代码](./src/__tests__/Client.test.ts)。

# 命令行使用

```bash
grpc-man <endpoint> <protoFilePath>

# for example:
grpc-man localhost:8080 /path/to/proto_file
```

# 本地运行

```bash
npm start <endpoint> <protoFilePath>

# for example:
npm start localhost:8080 /path/to/proto_file
```


## License
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2FJeff-Tian%2Fgrpc-man.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2FJeff-Tian%2Fgrpc-man?ref=badge_large)