操作DOM节点

| 获取DOM节点                     | 说明                              | 返回值            |
| ------------------------------- | --------------------------------- | ----------------- |
| domObj.children                 | 获取domObj的所有直属子节点        |                   |
| domObj.firstElementChild        | 获取domObj的第一个子节点          |                   |
| domObj.lastElementChild         | 获取domObj的最后一个子节点        |                   |
| domObj.getElementById()         | 通过id来获取dom节点               | domObj            |
| domObj.getElementsByTagName()   | 通过tagName来获取dom节点          | domObj组成的Array |
| domObj.getElementsByClassName() | 通过className来获取dom节点        | domObj组成的Array |
| domObj.querySelector()          | 通过css选择器语法获取第一个匹配接 | domObj            |
| domObj.querySelectorAll()       | 通过css选择器语法获取所有匹配节点 | domObj组成的Array |

| 更新DOM节点 | 说明                                                         |
| ----------- | ------------------------------------------------------------ |
| innerHTML   | 直接修改节点内容                                             |
| innerText   | 只能修改修改节点包含的text, 但无法获取或修改隐藏的节点       |
| textContent | 只能修改修改节点包含的text, 可以获取或修改隐藏的节点         |
| style       | 修改节点样式, 需要注意与css中的样式不同的是font-size需要写为fontSize |

| 插入节点                                              | 说明                                   | 返回值 |
| ----------------------------------------------------- | -------------------------------------- | ------ |
| parentElement.appendChild(domObj)                     | 把一个节点移动到父节点的最后一个子节点 | domObj |
| parentElement.insertBefore(domObj,  referenceElement) | 将domObj移动到referenceElement前       | domObj |

| 删除节点                 | 说明                                       | 返回值 |
| ------------------------ | ------------------------------------------ | ------ |
| parent.removeChild(self) | 需要通过父节点(parent)才能删除子节点(self) | self   |

