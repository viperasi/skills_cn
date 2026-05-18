---
name: migrate-to-shoehorn
description: 将测试文件从 `as` 类型断言迁移到 @total-typescript/shoehorn。当用户提到 shoehorn、想要在测试中替换 `as`，或需要部分测试数据时使用。
---

# 迁移到 Shoehorn

## 为什么使用 shoehorn？

`shoehorn` 让你在测试中传递部分数据，同时保持 TypeScript 满意。它以类型安全的替代方案替换 `as` 断言。

**仅测试代码。** 永远不要在生产代码中使用 shoehorn。

测试中使用 `as` 的问题：

- 被训练不去用
- 必须手动指定目标类型
- 对于故意错误的数据需要双重 `as`（`as unknown as Type`）

## 安装

```bash
npm i @total-typescript/shoehorn
```

## 迁移模式

### 只有少数几个属性需要的大对象

之前：

```ts
type Request = {
  body: { id: string };
  headers: Record<string, string>;
  cookies: Record<string, string>;
  // ...20 多个属性
};

it("通过 id 获取用户", () => {
  // 只关心 body.id，但必须伪造完整的 Request
  getUser({
    body: { id: "123" },
    headers: {},
    cookies: {},
    // ...伪造全部 20 个属性
  });
});
```

之后：

```ts
import { fromPartial } from "@total-typescript/shoehorn";

it("通过 id 获取用户", () => {
  getUser(
    fromPartial({
      body: { id: "123" },
    }),
  );
});
```

### `as Type` → `fromPartial()`

之前：

```ts
getUser({ body: { id: "123" } } as Request);
```

之后：

```ts
import { fromPartial } from "@total-typescript/shoehorn";

getUser(fromPartial({ body: { id: "123" } }));
```

### `as unknown as Type` → `fromAny()`

之前：

```ts
getUser({ body: { id: 123 } } as unknown as Request); // 故意用错类型
```

之后：

```ts
import { fromAny } from "@total-typescript/shoehorn";

getUser(fromAny({ body: { id: 123 } }));
```

## 何时使用每个

| 函数            | 用例                                     |
| --------------- | ---------------------------------------- |
| `fromPartial()` | 传递部分数据但仍通过类型检查             |
| `fromAny()`     | 传递故意错误的数据（保留自动补全）       |
| `fromExact()`   | 强制完整对象（稍后与 fromPartial 交换）  |

## 工作流

1. **收集需求** - 询问用户：
   - 哪些测试文件有引起问题的 `as` 断言？
   - 他们是否在处理只关心少数属性的大对象？
   - 他们是否需要为错误测试传递故意错误的数据？

2. **安装和迁移**：
   - [ ] 安装：`npm i @total-typescript/shoehorn`
   - [ ] 查找带 `as` 断言的测试文件：`grep -r " as [A-Z]" --include="*.test.ts" --include="*.spec.ts"`
   - [ ] 将 `as Type` 替换为 `fromPartial()`
   - [ ] 将 `as unknown as Type` 替换为 `fromAny()`
   - [ ] 添加来自 `@total-typescript/shoehorn` 的导入
   - [ ] 运行类型检查以验证
