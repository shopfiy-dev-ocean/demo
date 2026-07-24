# 项目编码规范

## 1.核心开发原则
 - **技术选型**:
    - **交互**:简单交互首选**Alpine.js**; 复杂独立组件使用 **WebComponents** (`customElements.define`)。
    - **尽量移除 jQuery**: 新增代码避免使用 jQuery。
    - **国际化(I18n)**:
        - 严禁硬编码用户可见文本。
        - 必须使用 `{{'key'|t}}` 并在 `locales/` 中维护翻译

## 2.Liquid最佳实践
- **性能与逻辑**:
    - 使用`{% render%}`替代`include`,以保证作用域隔离。
    - 避免在`for`循环中进行复杂查询或重计算。
    - 逻辑嵌套建议不超过3层,复杂逻辑需抽取为Snippet。
    - 高频变量应在文件顶部`assign`缓存,避免重复求值。
- **代码整洁**:
    - 必须使用`{%--%}`及其变体严格控制输出空白。
    - `{%schema%}`必须包含清晰的 `id`,`label`,`info`。

## 3.JavaScript与性能
- **资源优化**:
    - 图片必须使用 `lazysizes` (添加`lazyload`类), 避免首屏加载阻塞。
    - 非关键JS使用 `defer` 或 `async` 异步加载。
- **内存管理**:
    - 全局变量挂载至`window.theme`命名空间。
    - 必须监听`shopify:section:unload`事件并清理对应应的事件监听器,防止内存泄漏。
- **数据交互**:
    - 购物车及变体操作必须使用**Shopify AJAX API**,禁止整页刷新。
    - Alpine.js `x-data` 数据对象应保持轻量。

## 4.样式(CSS/SCSS)
- **组织结构**:
- **Scoped**: 组件特有样式直接写在 Liquid 文件内的 `<style>` 中。
- **Global**: 通用样式放入`assets/` 下的SCSS文件#。
- **命名规范**: 严格遵循**BEM**命名法(如`.block__element--modifier`),保持语义化。

## 5.命名约定速查
- **文件**: `kebab-case` (例:`custom-modal.liquid`）
- **Liquid变量**:`snake_case` (例:`vat_option_tiitle`）
- **JS 变量**: `camelCase` (例:`vatOptionsSelected`）
- **CSS类**:`kebab-case` + BEM (例:`.vat-option__title`）