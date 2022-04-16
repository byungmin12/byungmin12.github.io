# recursive components

프로젝트 진행 중 카테고리를 직접 만들기 위해 재귀를 사용해야했다.

하지만 카테고리 데이터가 고정적인 것이 아닌 가변적이었기 때문에 폴더를 눌렀을 때 데이터를 받아오고
폴더가 아닌 파일이었을 때는 파일의 데이터를 받아왔어여했다.

>

1. 폴더라면 UI적으로 폴더를 보여줘야함
2. 폴더의 자식데이터를 미리 다 가지고 오는 것이 아닌 폴더를 눌렀을 때 자식 데이터를 요청하고 받아와야함
3. 폴더를 파일보다 먼저 보여줘야함
4. 자식은 UI적으로 파일로 보여줘야함

## 코드

```js

function sortIsDir(data: Data[]): Data[] | [] {
  let result = [
    ...data.filter((el) => el.is_dir),
    ...data.filter((el) => !el.is_dir),
  ];
  return result as Data[] | [];
}

function ParentNode({ title }: { title: string }) {
  const [isOpen, setIsOpen] = React.useState(false);
  const [data, setData] = React.useState<Data[]>([]);

  const recursiveNode = React.useCallback(() => {
    // 요청을 보내고 받아와야함
    // 임시 setTimeout을 사용
    setTimeout(() => {
      setData(
        sortIsDir([
          {
            path: "model/MLmodel",
            is_dir: false,
            file_size: 380,
          },
          {
            path: "model/conda.yaml",
            is_dir: false,
            file_size: 134,
          },
          {
            path: "model/data",
            is_dir: true,
          },
        ])
      );
    }, 100);

    return data.length > 0 ? <Tree data={data} /> : <div>no data</div>;
  }, [data]);
  return (
    <>
      <span
        onClick={() => {
          setIsOpen(!isOpen);
        }}
      >
        {isOpen ? <ArrowRightOutlinedIcon /> : <FolderOpenOutlinedIcon />}
        parent --- {title}
      </span>
      {isOpen && <div>{recursiveNode()}</div>}
    </>
  );
}

// 여기서 받는 데이터는 처음 받는 데이터임
// 처음받은 데이터란 root페이지가 렌더 되었을 때 받은 데이터
function Tree({ data }: ITreeProps) {
  const setIsContentOpen = useSetRecoilState(contentOpenState);

  return (
    <Root>
      {sortIsDir(data).map((el: Data, idx: number) => {
        if (el.is_dir) {
          return <ParentNode title={el.path} key={idx} />;
        } else {
          return (
            // 자식은 그냥 div 태그입니다.
            <Child
              key={idx}
              onClick={() => {
                setIsContentOpen(true);
              }}
            >
              <InsertDriveFileOutlinedIcon />
              {el.path}
            </Child>
          );
        }
      })}
    </Root>
  );
}
```

## 요약

코드는 정리가 안된 상태라 매우 난잡하지만

> 1 . 렌더링 되었을 때 데이터를 tree로 전달 2. tree에서 받은 데이터는 폴더를 앞으로 파일을 뒤로 이동 3. 그 후 반복문을 통해 자식과 부모를 나뉨 4. 부모 컴포넌트는 폴더이므로 **열렸을 때** api요청을 보냄 5. 여기서 api요청은 useCall을 통해 열렸을 때 작동하게 함 6. useCallback의 callback함수의 리턴값을 tree컴퍼넌트를 함
