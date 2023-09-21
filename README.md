# InternProject


# https://asecurity.dev/entry/Python-%EB%AC%B4%EB%A3%8C%EB%A1%9C-%EC%82%AC%EC%9A%A9%ED%95%A0-%EC%88%98-%EC%9E%88%EB%8A%94-%EB%B2%88%EC%97%AD-API-TOP-4
# https://asecurity.dev/entry/Python-googletrans-Type-None-%EC%98%A4%EB%A5%98-%ED%95%B4%EA%B2%B0
# https://github.com/ssut/py-googletrans


https://meta.stackexchange.com/questions/84352/can-i-crawl-stackoverflow-articles

https://archive.org/details/stackexchange
- stackoverflow의 데이터 dump파일 받을 수 있는 사이트
- 관련 자세한 내용:
    1. Posts.xml: 이 파일은 Stack Overflow의 질문과 답변 데이터를 포함하고 있습니다. 각 게시물(post)은 게시물 유형(질문 또는 답변), 작성일, 본문 등과 같은 여러 속성을 가지고 있습니다.
    2. Comments.xml: 이 파일은 각 질문과 답변에 대한 댓글 데이터를 포함하고 있습니다. 댓글 데이터는 댓글의 내용, 작성일, 댓글이 달린 게시물 ID 등의 정보를 가지고 있습니다.
    
    

https://huggingface.co/datasets/lvwerra/stack-exchange-paired



def data_save():

    df = pd.read_parquet('./0000.parquet', engine = 'pyarrow')


    sp_df = pd.DataFrame({},columns=['en_text'])
    sp_df['en_text'] = df['question'].sample(n=50400).reset_index(drop=True)



    mask = sp_df.applymap(lambda x: '\u001F' in str(x))
    filtered_rows = sp_df[mask.any(axis=1)]
    print(filtered_rows)
    if filtered_rows.empty:
        print("hi")

        sp_df['en_text'] = sp_df['en_text'] + '\u001F'

        # 코드 데이터이기 때문에 쉼표, 따옴표등 csv파일로 저장하기 까다로운 요소들이 많다 그래서 구분자를 정해주자.
        sp_df.to_csv('./sample_output.csv',index=False,sep='\u001F')
    
    
    output_df = pd.read_csv('./sample_output.csv')
    output_df['en_text'] = output_df['en_text'].astype(str).str.replace('', '')  # '#' 문자를 삭제
    output_df.to_csv('./sample_output.csv',index=False)

----


# output_df = pd.read_csv('./sample_output.csv')

# output_df.loc[0:2, 'ko_text'] = output_df.loc[0:2, 'en_text'].apply(n_trans)
# output_df.to_csv('./sample_output.csv',index=False)





# https://asecurity.dev/entry/Python-%EB%AC%B4%EB%A3%8C%EB%A1%9C-%EC%82%AC%EC%9A%A9%ED%95%A0-%EC%88%98-%EC%9E%88%EB%8A%94-%EB%B2%88%EC%97%AD-API-TOP-4
# https://asecurity.dev/entry/Python-googletrans-Type-None-%EC%98%A4%EB%A5%98-%ED%95%B4%EA%B2%B0
# https://github.com/ssut/py-googletrans
