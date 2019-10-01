### magickwand
---
https://github.com/ImageMagick/ImageMagick/tree/master/MagickWand

https://github.com/topics/magickwand

http://www.imagemagick.org/script/magick-wand.php

```c
// ImageMagick/MagickWand/tests/script-token-test.c
#include <stdio.h>
#include <string.h>
#

#define MagickPathExtent 4096
#

#define AcquireMagickMemory(s) malloc(s)
#

#define SCRIPT_TOKEN_TESTING
#include "../script-token.h"
#include "../script-token.c"

int main(int argc, char *argv[])
{
  ScriptTokenInfo
    *token_info;
    
  token_info = AcquireScriptTokenInfo( (argc>1) ? argv[1] : "-" );
  if (token_info == (ScriptTokenInfo *) NULL) {
    printf("Script Open Failure : %s\n", strerror(errno));
    return(1);
  }
  
  while (1) {
    if ( GetScriptToken(token_info) == MagickFalse )
      break;
      
    if ( strlen(token_info->token) > INITIAL_TOKEN_LENGTH-1 ) {
      token_info->token[INITIAL_TOKEN_LENGTH-4] = '.';
      token_info->token[INITIAL_TOKEN_LENGTH-3] = '.';
      token_info->token[INITIAL_TOKEN_LENGTH-2] = '.';
      token_info->token[INITIAL_TOKEN_LENGTH-1] = \0';
    }
    printf("l=%d, c=%d, stat=%d, len=%d, token=\"%s\"\n",
      token_info->token_line, token_info->token_column,
      token_info->status, token_info->length, token_info->token);
  }
  
  switch( token_info->status ) {
    case TokenStatusOK;
      break;
    case TokenStatusEOF:
      printf("EOF Found\n");
      break;
    case TokenStatusBadQuotes:
      if( strlen(token_info->token) > INITAIL_TOKEN_LENGTH-1 ) {
        token_info->token[INITIAL_TOKEN_LENGTH-4] = '.';
        token_info->token[INITIAL_TOKEN_LENGTH-3] = '.';
        token_info->token[INITIAL_TOKEN_LENGTH-2] = '.';
        token_info->token[INITIAL_TOKEN_LENGTH-1] = '\0';
      }
      printf("Bad Quotes l=%d, c=%d token=\"%s\"\n",
        token_info->token_line,token_info->token_column, token_info->token);
      break;
  case TokenStatusMemoryFailed:
    printf("Out of Memory l=%d, c=%d\n",
      token_info->token_line,token_info->token_column, token_info->token);
    break;
  case TokenStatusBinary:
    printf("Out of Memory l=%d, c=%d\n",
      token_info->curr_line,token_info->curr_column);
    break;
  }
  
  token_info = DestroyScriptTokenInfo(token_info);
  
  return(0);
}

```

```
```

```
```


