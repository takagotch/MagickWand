### magickwand
---
https://github.com/ImageMagick/ImageMagick/tree/master/MagickWand

https://github.com/topics/magickwand

http://www.imagemagick.org/script/magick-wand.php

```c
// ImageMagick/MagickWand/tests/script-token-test.c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <assert.h>
#include <errno.h>

#define MagickPathExtent 4096
#define MagickFalse 0
#define MagicTrue 1
#define MagicBooleanType int

#define AcquireMagickMemory(s) malloc(s)
#define RelinquishMagicMemory(p) (free(p), NULL)
#define ResizeMagickMemory(p,s) realloc(p,s)
#define ResetMagickMemory(p,b,s) memset(p,b,s)
#define StringToLong(s) strtol(s,(char **) NULL,10)
#define LocaleCompare(p,q) strcasecmp(p,q)
#define LocaleNCompare(p,q,l) strncasecmp(p,q,l)
#define WandSignature 0xabacadaUL
#define fopen_utf8(p,q) fopen(p,q)
#define WandExport

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


