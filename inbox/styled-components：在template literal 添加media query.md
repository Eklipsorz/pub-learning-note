## 描述


```
import React from 'react';
import styled from 'styled-components';
import './Button.css';

const Button = styled.button`
  width: 10%;
  font: inherit;
  padding: 0.5rem 1.5rem;
  border: 1px solid #8b005d;
  color: white;
  background: #8b005d;
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.26);
  cursor: pointer;

  &:focus {
    outline: none;
  }

  &:hover,
  &:active {
    background: #ac0e77;
    border-color: #ac0e77;
    box-shadow: 0 0 8px rgba(0, 0, 0, 0.26);
  }

  @media (min-width: 768px) {
    width: auto;
  }
`;

// const Button = (props) => {
//   return (
//     <button type={props.type} className='button' onClick={props.onClick}>
//       {props.children}
//     </button>
//   );
// };

export default Button;

```

## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]- [[CSS]]
Links:
[[media query 是定義一系列問題來向瀏覽器詢問裝置是否為指定裝置、解析度是否為指定解析度，若是的話，就會以定義好的樣式屬性來渲染]]
References: