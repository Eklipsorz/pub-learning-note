## 描述


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




```
.backdrop {
  /* position */
  position: fixed;
  top: 0;
  left: 0;
  z-index: 10;

  /* display */
  display: block;

  /* box model */
  width: 100%;
  height: 100%;

  /* font or other */
  background-color: rgba(0, 0, 0, 0.8);
}

.modal {
  /* position */
  position: fixed;
  top: 15vh;
  left: 35%;
  z-index: 99;

  /* display */
  /* box model */
  width: 30%;
 疑似解決點 -> overflow: hidden;
  /* font or other */
}

.modal-body {
  /* position */
  /* display */
  /* box model */
  padding: 1rem;
  /* font or other */
  background: #fff;
}

.modal-header {
  /* position */
  /* display */
  /* box model */
  padding: 0.1rem 1rem;
  /* font or other */
  color: #fff;
  background: #4b0b56;
}

.modal-footer {
  /* position */
  /* display */
  display: flex;
  justify-content: flex-end;
  /* box model */
  padding: 1rem;
  /* font or other */
  background: #fff;
}

```

## 複習


---
Status: #🌱 #📓 
Tags:
[[CSS]]
Links:
References: