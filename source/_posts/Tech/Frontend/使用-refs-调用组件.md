---
title: 使用 refs 调用组件
tags: React
abbrlink: c543f67c
date: 2022-05-29 16:53:38
categories:
---

话不多说，先上代码
<!--more-->

# Class

```tsx
type ModalStates = {
  visible: boolean;
};

class MyClassModal extends React.Component<any, ModalStates> {
  constructor(props: any) {
    super(props);
    this.state = {
      visible: false,
    };

    this.openModal = this.openModal.bind(this);
    this.closeModal = this.closeModal.bind(this);
  }

  openModal() {
    this.setState({ visible: true });
  }

  closeModal() {
    this.setState({ visible: false });
  }

  render() {
    const { visible } = this.state;

    return (
      <>
        <Modal
          title="My Class Modal"
          visible={visible}
          onOk={this.closeModal}
          onCancel={this.closeModal}
        >
          <p>Class Component</p>
        </Modal>
      </>
    );
  }
}

class MyClassApp extends React.Component<any, any> {
  modal: RefObject<MyClassModal>;

  constructor(props: any) {
    super(props);

    this.modal = React.createRef<MyClassModal>();
    this.openModal = this.openModal.bind(this);
  }

  openModal() {
    this.modal.current?.openModal();
    console.log(this.modal);
  }

  render() {
    return (
      <div>
        <Button type="primary" onClick={this.openModal}>
          Open Class Modal
        </Button>
        <MyClassModal ref={this.modal} />
      </div>
    );
  }
}
```

# Function
```tsx
const MyFunctionModal = React.forwardRef<MyFunctionModalRefs, any>((props, ref) => {
  const [visible, setVisible] = useState(false);

  useImperativeHandle(ref, () => ({ openModal }));

  const openModal = () => {
    setVisible(true);
  };

  const closeModal = () => {
    setVisible(false);
  };

  return (
    <>
      <Modal title="My Function Modal" visible={visible} onOk={closeModal} onCancel={closeModal}>
        <p>Function Component</p>
      </Modal>
    </>
  );
});

const MyFunctioncApp: React.FC = () => {
  const ref = createRef<MyFunctionModalRefs>();

  const openModal = () => {
    console.log(ref);
    ref.current?.openModal();
  };

  return (
    <div>
      <Button type="primary" onClick={openModal}>
        Open Function Modal
      </Button>
      <MyFunctionModal ref={ref} />
    </div>
  );
};
```