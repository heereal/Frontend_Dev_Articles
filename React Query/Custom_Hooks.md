# React Query Custom Hooks로 사용하기
> [React Query Custom Hooks로 더 잘 사용해보기](https://medium.com/hcleedev/web-react-query-custom-hooks%EB%A1%9C-%EB%8D%94-%EC%9E%98-%EC%82%AC%EC%9A%A9%ED%95%B4%EB%B3%B4%EA%B8%B0-2ea47fb358c3)

<br/>

## useQuery
```javascript
export const userInfoQueryKey = 'userInfoQueryKey';
export const useUserInfoQuery = (id: number) => {
  return useQuery([userInfoQueryKey, id], api.get('/user', { id }));
}
```
- `userInfoQueryKey`는 이런 식으로 Custom Hook과 붙여둘 수도 있고, 그냥 Query Key만 모아두는 파일을 따로 사용할 수도 있다.

<br/>

## useMutation
```javascript
export interface CreateUserRequest {
  name: string;
  id: number;
}

export const useCreateUserMutation = (successCallback: () => void) => {
  return useMutation((data: CreateUserRequest) => api.post('/user', {...data}), {
    onSuccess: successCallback,
  });
}
```
- 데이터 변경 요청이 성공했을 경우에 실행할 callback 함수를 전달한다.

<br/>

## Invalidate Query
```javascript
import { UserInfoQueryKey } from 'somewhere';

const useCreateUserMutation = (successCallback: () => void) => {
  const client = useQueryClient();

  return useMutation((data: CreateUserRequest) => api.post('/user', {...data}), {
    onSuccess: () => {
      client.invalidateQueries(UserInfoQueryKey)
        .then(() => successCallback());
  });
}
```
- `onSuccess` 내에서 `client.invalidateQueries(UserInfoQueryKey)`를 불러서 해당 Key에 대한 캐싱 데이터를 Invalidate한다.




