
## Error : CLEARTEXT communication to XXXX not permitted by network security policy
- Base Url 에 **https**가 아닌 http를 쓰면 `CLEARTEXT communication to XXXX not permitted by network security policy` 오류가 난다.


## Path
 
- https://example.com/user/4z7l 인 경우 : @Path 사용
```kotlin
interface UserService {
    @GET("users/{name}")
    fun getUser(
        @Path("name") userName: String
    ): Call<User>
}
```

- https://example.com/user?q=4z7l 인 경우 : @Query 사용
```kotlin
interface UserService {
    @GET("users")
    fun getUser(
        @Query("q") userName: String
    ): Call<User>
}
```



<br><br>
> :bookmark: __REFERENCE__<br>
https://square.github.io/retrofit/
