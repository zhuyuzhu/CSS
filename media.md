

# 媒体查询@media



```css

@media (min-width: 1024px){
    #login_header .sys_logo .logo_title{
        font-size: 18px
    }
}

@media (min-width: 1280px) {
    #login_header .sys_logo .logo_title{
        font-size: 22px;
    }
}

@media (min-width: 1366px) {

    #login_header .sys_logo .logo_title{
        font-size: 42px;
    }
}  

@media (min-width: 1440px) {
    #login_header .sys_logo .logo_title{
        font-size: 48px;
    }
} 

@media (min-width: 1680px) {
    #login_header .sys_logo .logo_title{
        font-size: 54px;
    }
} 
@media (min-width: 1920px) {
    #login_header .sys_logo .logo_title{
        font-size: 64px;
    }
}
```





这样以来，如果比1024大，就使用1024的样式。比1280大，就使用1280的样式。以此类推。

全屏时使用以上值。非全屏时，使用比实际屏幕小的是值。

