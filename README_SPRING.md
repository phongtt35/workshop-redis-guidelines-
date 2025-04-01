## Docker
Pull image
```
docker pull redis
```
Run container
```
docker run -d --name redis -p 6372:6372 redis:latest
```

## Dependency
```
<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-cache</artifactId>
</dependency>

 <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

## Appication.properties
```
spring.redis.host=localhost
spring.redis.port=6379
```

## Bean Configuration
```
    @Bean
    public CacheManager cacheManager(RedisConnectionFactory connectionFactory) {
        RedisCacheConfiguration redisCacheConfiguration = RedisCacheConfiguration.defaultCacheConfig()
                .serializeKeysWith(RedisSerializationContext.SerializationPair.fromSerializer(new StringRedisSerializer()))
                .serializeValuesWith(RedisSerializationContext.SerializationPair.fromSerializer(new GenericJackson2JsonRedisSerializer()));

        return RedisCacheManager.builder(connectionFactory)
                .cacheDefaults(redisCacheConfiguration)
                .build();
    }

    @Bean
    public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory factory) {
        RedisTemplate<String, Object> template = new RedisTemplate<>();
        template.setConnectionFactory(factory);
        return template;
    }
```

## Annotation
Lưu cache
```
@Cacheable(value = "...", key = "'...'")
```
Xóa cache
```
@CacheEvict(value = "...", key = "'...'")
```
Cập nhập cache
```
@CachePut(value = "...", key = "'...'")
```
