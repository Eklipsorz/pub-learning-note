## 描述

### components 元件目錄分得太細

原本是每個元件各為一個目錄，比如
```
components 目錄：
	- UI 子目錄
	- UserInfoForm 子目錄
	- UserInfoList 子目錄
	- UserInfoList 子目錄
```

在這裡，可以修改成根據元件所要針對的資源為主，在這可以分為通用元件UI和使用者：
```
components 目錄：
	- UI 子目錄
	- Users 子目錄
```

### modal 可以額外再切分

modal 部分可以切分成backdrop和 modal部分：
	- backdrop部分是負責modal所在的背景
	- modal部分負責對話視窗部分
這樣切分的好處是：
	- 切分出更多可重複使用的元件


#### 原版本-modal和backdrop合在一起
```
import Button from './Button';
import styles from './ErrorModal.module.css';

const ErrorModal = (props) => {
  const { title, text } = props;

  const clickHandler = (event) => {
    props.onErrorModal();
  };

  return (
    <div className={styles['modal']} onClick={clickHandler}>
      <div className={styles['modal-content']}>
        <div className={styles['modal-header']}>
          <h2>{title}</h2>
        </div>
        <div className={styles['modal-body']}>
          <p>{text}</p>
        </div>
        <div className={styles['modal-footer']}>
          <Button onClick={clickHandler}>Okay</Button>
        </div>
      </div>
    </div>
  );
};

export default ErrorModal;

```

#### 第二版本-modal和backdrop分開來

```
import Button from './Button';
import styles from './ErrorModal.module.css';
import Card from '../UI/Card';
const ErrorModal = (props) => {
  return (
    <>
      <div className={styles['backdrop']} onClick={props.onConfirm}></div>
      <Card className={styles['modal']}>
        <div className={styles['modal-header']}>
          <h2>{props.title}</h2>
        </div>
        <div className={styles['modal-body']}>
          <p>{props.text}</p>
        </div>
        <div className={styles['modal-footer']}>
          <Button onClick={props.onConfirm}>Okay</Button>
        </div>
      </Card>
    </>
  );
};

export default ErrorModal;
```

## 複習


---
Status: #🌱 #📓 
Tags:
Links:
[[modal 是一個專門與使用者互動並從互動中將資訊傳遞給主程式，其結構為存放背景、對話視窗，製作方式請詳讀本文章]]
[[React - modal 實作案例]]
References: