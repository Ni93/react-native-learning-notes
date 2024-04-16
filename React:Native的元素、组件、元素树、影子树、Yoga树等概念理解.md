# React Element - React 元素

**`React` 元素** 是一个普通的对象。

* 描述 `DOM` 节点及节点属性；

* 描述组件及组件属性。

对象携有 `type: (string | ReactClass)` 和 `props: Object` 字段。

```
{
  type: string | ReactClass
  props: Object
}
```


### DOM 元素

```
<button className='button button-blue'>
  <b>
    OK!
  </b>
</button>
```

用对象描述 DOM

```
{
  type: 'button',
  props: {
    className: 'button button-blue',
    children: {
      type: 'b',
      props: {
        children: 'OK!'
      }
    }
  }
}
```


### 组件元素

```
<Button color='blue'>
  OK
</Button>
```

用对象描述组件

```
{
  type: Button,
  props: {
    color: 'blue',
    children: 'OK!'
  }
}
```

**一个用于描述组件的元素也是一个元素，就像一个用于描述 `DOM` 节点的元素一样。它们可以彼此嵌套，互相混合。**

```
function Header() {
  return (
    <header>
      <h1>Header</h1>
    </header>
  )
}

function Main() {
  return (
    <div>
      <Header />
      <p>这是一段内容</p>
    </div>
  )
}
```

`Header` 组件用对象描述

```
{
  type: 'header',
  props: {
    children: {
      type: 'h1',
      props: {
        children: 'Header',
      },
    },
  },
}
```

`Main` 组件用对象描述

```
{
  type: 'div',
  props: {
    children: [
      {
        type: 'header',
        props: {
          children: {
            type: 'h1',
            props: {
              children: 'Header',
            },
          },
        },
      }, // {type: 'Header', props: {}}
      {
        type: 'p',
        props: {
          children: '这是一段内容',
        },
      },
    ],
  },
}
```

`React` 将知道页面上每一个组件之下的 `DOM` 标签元素。

### 术语表

* **`React Element`:** `React` 元素


# React Component - React 组件

A JavaScript function or class that instructs *[描述]* how to create a **React Element**.

**`React` 组件** 就是 **`JavaScript` 函数或者类**，描述如何创建 **`React` 元素**。

函数组件

```
function Welcome(props: {name: string}) {
  return (
    <View>
      <Text>Hello {props.name}</Text>
    </View>
  )
} 
```

类组件

```
class Welcome extends React.Component<{name: string}, any> {
  constructor(props) {
    super(props)
  }

  render() {
    return (
      <View>
        <Text>Hello {this.props.name}</Text>
      </View>
    )
  }
}
```

### 术语表

* **`React Element`:** `React` 元素


# React Composite Components - React 组合组件

**React Components** with render implementations that reduce to other **React Composite Components** or **React Host Components**.

(**`React` 组件** 的渲染实现可以简化为其他 **`React` 组合组件** 或 **`React` 宿主组件**。)

组合组件示例

```
function Welcome(props: {name: string}) {
  return (
    <View>
      <Text>Hello {props.name}</Text>
    </View>
  )
} 
```

### 术语表

* **`React Composite Components`:** `React` 组合组件
* **`React Host Components`:** `React` 宿主组件


# React Host Components or Host Components (React 宿主组件或者宿主组件)

React Components whose view implementation is provided by a host view (e.g., `<View>`, `<Text>`). 

(由宿主视图提供视图实现的 **`React` 组件**，例如 `<View>`, `<Text>`。)

On the Web, ReactDOM's Host components would be components like `<p>` and `<div>`.

(在 `Web` 端，`ReactDOM` 的宿主组件会是像 `<p>` 和 `<div>`。)

React Native 宿主组件示例：

* `<View>`
* `<Text>`


React Dom 宿主组件示例：

* `<p>`
* `<div>`


# React Element Tree (and React Element) - React 元素树 (和 React 元素)

A **React Element Tree** is created by React in JavaScript and consists of **React Elements**. 

(**`React` 元素树** 是由 `JavaScript` 中的 `React` 创建的，**`React` 元素树** 由 **`React` 元素** 组成。)

A **React Element** is a plain JavaScript object that describes what should appear on the screen. 

(一个 **`React` 元素** 是一个普通的 `JavaScript` 对象，**`React` 元素** 描述了应该在屏幕上展示什么)

It includes props, styles, and children.

(**`React` 元素** 包含 `props, styles, and children`)

**React Elements** only exist in JavaScript and can represent  instantiations of either **React Composite Components** or **React Host Components**.

(**`React` 元素** 只存在于 `JavaScript`，可以表示 **`React` 组合组件** 实例或 **`React` 宿主组件** 实例)

### 术语表

* **`React Element Tree`:** `React` 元素树
* **`React Element`:** `React` 元素
* **`React Composite Components`:** `React` 组合组件
* **`React Host Components`:** `React` 宿主组件


# React Shadow Tree (and React Shadow Node) - React 影子树 (和 React 影子节点)

A **React Shadow Tree** is created by the **Fabric Renderer** and consists of *[由......组成]* **React Shadow Nodes**.

(**`React` 影子树** 是由 **`Fabric` 渲染器** 创建的，**`React` 影子树** 由 **`React` 影子节点** 组成。)

A **React Shadow Node** is an object that represents *[代表]* a **React Host Component** to be mounted, and contains props that originate from *[来源]* JavaScript. 

(一个 **`React` 影子节点** 是一个对象，他代表一个要挂载的 **`React` 宿主组件**， 并且包含来自 `JavaScript` 的 `props`。)

They also contain layout information (x, y, width, height). 

(**`React` 影子节点** 也包含布局信息，`x, y, width, height`。)

In **Fabric**, **React Shadow Node** objects exist in C++. 

(在 **`Fabric`** 中，**`React` 影子节点** 对象存在于 `C++` 中。)

Before **Fabric**, these existed in the mobile runtime heap (e.g. Android JVM).

(在 **`Fabric`** 之前，它们存在于手机运行时的堆栈中，比如 `Android JVM`。)

### 术语表

* **`Fabric Renderer`:** `Fabric` 渲染器
* **`React Shadow Tree`:** `React` 影子树
* **`React Shadow Nodes`:** `React` 影子节点
* **`React Host Component`:** `React` 宿主组件


# Yoga Tree (and Yoga Node) - Yoga 树 (和 Yoga 节点)

The **Yoga Tree** is used by [**Yoga**](https://www.yogalayout.dev/) to calculate layout information for a **React Shadow Tree**.

（**`Yoga` 树** 被 **`Yoga`** 用来计算 **`React` 影子树** 的布局信息。）

Each **React Shadow Node** typically *[一般，通常]* creates a **Yoga Node** because **React Native** employs *[使用]* **Yoga** to calculate layout. 

（每个 **`React` 影子节点** 通常会创建一个 **`Yoga` 节点**，因为 **`React Native`** 使用 **`Yoga`** 来计算布局。）

However, this is not a hard requirement. 

（然而，这并不是一个硬性要求。）

**Fabric** can also create **React Shadow Nodes** that do not use **Yoga**; the implementation of each **React Shadow Node** determines *[决定，控制]* how to calculate layout.

（**`Fabric`** 也可以创建不使用 **`Yoga`** 的 **`React` 影子节点**；每个 **`React 影子节点`** 的实现决定了如何计算布局。）

### 术语表

* **`Yoga Tree`:** `Yoga` 树
* **`Yoga Node`:** `Yoga` 节点
* **`React Shadow Tree`:** `React` 影子树
* **`React Shadow Node`:** `React` 影子节点