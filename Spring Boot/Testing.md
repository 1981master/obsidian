<mark>Mokito JUnit5</mark>
```java
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import static org.mockito.Mockito.*;
import static org.assertj.core.api.Assertions.assertThat;

public class UserServiceTest {

    @Mock
    private UserRepository userRepository;

    @InjectMocks
    private UserService userService;

    @Test
    public void testFindUserById() {
        // Arrange: Set up the mock behavior
        User mockUser = new User(1L, "John Doe");
        when(userRepository.findById(1L)).thenReturn(Optional.of(mockUser));

        // Act: Call the method we want to test
        User result = userService.findUserById(1L);

        // Assert: Verify the result
        assertThat(result).isNotNull();
        assertThat(result.getName()).isEqualTo("John Doe");
    }
}

```