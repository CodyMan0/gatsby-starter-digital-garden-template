# state 정리

- ### editor
	const [formNum, setFormNum] = useRecoilState(formNumState)
	-> formlist 안에 있는 리스트들이 몇개 있는지 세주는 역할 ==1. (전역)==
	- ### optionbox
		const setFormList = useSetRecoilState(formListState);
		-> ==2.== 4개의 텝을 눌렀을때 데이터가 넘어갈 수 있도록 하기 위해 ==2.(전역)==
		==1== 번 전역 불러와서 obtionbox누를때 +1 되도록 했다. 
		- ### surveyEditor
		const [formList, setFormList] = useRecoilState(formListState);
		-> ==2== 전역에서 가져왔다. optionbox를 눌러추가된 애들이 원하는 필드에 그려지도록 하였다. 
		- ### 4가지 질문 컴포넌트
		==2==번 을 전역에서 가지고 왔다. ->  formList의 순서를 배열로 받기 위해서!! object.keys를 사용해보려고 했다.
			### GlobalQuestion 컴포넌트
			==2== formList를 가지고 왔다. 여기서 삭제기능을 구현하려고 했다. 휴지통 누르면 formList에서 같은 id 값을 가지고 있는 것은 빼려고 했다 여기서 문제 -> 5개의 질문을 만들면 sortIndex는 5 인것이 문제!! 이게 배열로 있어야 form.id와 비교 
			-> 그래서 object.key를 사용해서 배열로 받아야할 것 같다. 
			-> 아니다 한 컴포넌트 위에서 관리를 해야하는 것 같다 배열로 해도 [1], [2,] [3] 으로 되고 있다. 내가 원하는 것은 [1,2,3,4,5]